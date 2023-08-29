reflex

```
int Slave::ZAxis::Zero(int timeout)
{
    CHECK_SIMULATE_WITH_RET(DPtr->mSimulate)

    INIT_EMPTY_CALLBACK;
    auto ptr = ZAxisPtr;
    auto seq = ptr->Zero(resultCallback, nullptr, timeout + ptr->mZAxisSysParams.zero_time_out * 1000);
    bool ret = ptr->waitForResult(seq);
    LogDebug << "ret " << ret << " msgState: " << (int)msgState;
    return msgState;
}
```



```
#define CHECK_SIMULATE_WITH_RET(X)  if(X) \
    { \
        LogDebug << "模拟环境"; \
        boost::this_thread::sleep(boost::posix_time::millisec(100)); \
        return 0; \
    }
```



```
#define DPtr            Slave::GetInstance().d_ptr
```



```
#define INIT_EMPTY_CALLBACK uint16_t msgState = heygears::Command_SendFailed; \
    ByteArray recvData; \
    auto resultCallback = [&msgState, &recvData](const uint16_t state, const ByteArray &data){ msgState = state; \
    recvData = data;\
    }
```



```
#define ZAxisPtr        DPtr->mSlaveDevice->zAxis()
```



```
    // 命令  sdk自定义错误码，不是下位机返回的
    Command_NoTimeout          = 0x0110,
    Command_AckTimeout         = 0x0111,
    Command_ResultTimeout      = 0x0112,
    Command_Cancel             = 0x0113,
    Command_SendFailed         = 0x0114,
```



```
int ZAxis::Zero(const ResultCallBack &resultCallback, const CmdCallBack &cmdCallback, int timeout)
{
    std::vector<uint8_t> params{};
    SEND_PACKET_WITH_CMDCB(CmdAxis::ZERO_MOTION_BYFORCE, true, true);
    return msgPtr->mSeq;
}
```



```
#define SEND_PACKET_WITH_CMDCB(CMD, NEED_ACK, NEED_RESULT) auto msgPtr = makeMsgPtr(mComponent, CMD, FrameType_CMD, params,  \
    mDevice->getSeq(), NEED_ACK,    \
    NEED_RESULT, resultCallback, timeout, cmdCallback);   \
    mDevice->sendMsg(msgPtr)
```



```
enum CmdAxis:uint8_t
{
    QUERY_PARAMS        = 0x01,     ///< 查询主轴参数
    CONFIG_PARAMS       = 0x21,     ///< 配置主轴参数
    STOP_MOTION         = 0x61,     ///< 紧急停止
    LOCK_MOTION         = 0x62,     ///< 动作锁，1表示已经锁死，不能再动
    RELATIVE_MOTION     = 0x63,     ///< 相对定位       
    RESET_MOTION        = 0x64,     ///< 主轴复位
    ZERO_MOTION_BYFORCE = 0x65,     ///< 压力寻零
    PRESS_KNIFE         = 0x66,     ///< 压力寻铲
    SEGMENTED_MOTION    = 0x67,     ///< 分段点动 参数1：1=上升 2=下降
    SEGMENTED_PARAMSV2  = 0x68,     ///< 分段点动参数设置
    HEAT_MIX_CTRL       = 0x69,     ///< 搅拌控制
    LOCATE_MOTION       = 0x6A,     ///< 绝对定位
    QUERY_HEIGHT        = 0x6B,     ///< 查询高度
    ROUGH_ADJUST        = 0x6C,     ///< 粗略调平
    PRECISE_ADJUST      = 0x6D,     ///< 精准调平
};
```



```
// 帧类型
enum FrameType: uint8_t
{
    FrameType_CMD    = 0x01,    ///< 指令
    FrameType_ACK    = 0x02,    ///< ack
    FrameType_RESULT = 0x03,    ///< 结果返回
    FrameType_INFO   = 0x04,    ///< 通知
};
```



```
    template<class T>
    DeviceMsgPtr makeMsgPtr(uint8_t component, uint8_t cmd, uint8_t frameType, const T params, uint16_t seq, bool needAck = false, \
                            bool needResult = false, const ResultCallBack &resultCallback = nullptr, \
                            int timeout = 3000, const CmdCallBack &cmdCallback = nullptr)
    {
        DeviceMsgPtr msgPtr(new heygears::DeviceMsg());
        msgPtr->mSeq = seq;
        msgPtr->mMsgName = getFuncCodeString(component, cmd);
        msgPtr->mReqMessage = GenRawCmd(msgPtr->mSeq, frameType, component, cmd, 0, params);
        msgPtr->mNeedAck = needAck;
        msgPtr->mNeedResult = needResult;
        msgPtr->mResultCallBack = resultCallback;
        msgPtr->mResultTimeout = timeout;
        msgPtr->mCmdCallBack = cmdCallback;

        return msgPtr;
    }
```



```
class DeviceMsg
{
public:
    enum TimeoutType
    {
        NoTimeout = 0x0110, ///< 没有超时
        AckTimeout,         ///< ack超时
        ResultTimeout,      ///< 结果超时
        CommandCancel,      ///< 取消打印
    };

public:
    DeviceMsg();

    // 检查超时
    TimeoutType checkTimeout(int ackTimeout);

public:
    int64_t mResultTimeout = 3000;              ///< 结果等待超时时间戳
    ResultCallBack mResultCallBack = nullptr;   ///< 结果接收回调
    CmdCallBack mCmdCallBack = nullptr;         ///< 命令闭环回调
    std::chrono::time_point<std::chrono::steady_clock>
    mSendTimePoint;                             ///< 发送时间戳

    std::string mMsgName = "unknown";           ///< 消息名称

    ByteArray mReqMessage;                      ///< 发送的数据
    ByteArray mRecvMessage;                     ///< 接收的数据

    uint16_t   mSeq;                        ///< 流水号
    uint16_t   mID;                         ///< 命令id

    uint8_t mSendCnt = 0;                   ///< 已发送次数

    bool mNeedAck = false;                  ///< 需等待ack
    bool mAlreadyAck = false;               ///< 已接收到ack
    bool mAlreadyAckTimeout = false;        ///< 已经ack超时

    bool mNeedResult = false;               ///< 需等待结果
    bool mAlreadyResult = false;            ///< 已接收到结果
    bool mAlreadyResultTimeout = false;     ///< 已经结果超时
};
```



```
using DeviceMsgPtr = std::shared_ptr<DeviceMsg>;
```



```
std::string getFuncCodeString(uint8_t deviceType, uint8_t deviceFunc)
{
    uint16_t funcCode = deviceType << 8 | deviceFunc;
    auto iter = funcCodeMap.find(funcCode);
    if(iter != funcCodeMap.end())
        return iter->second;
    else
    {
        switch(deviceType)
        {
        case SYS:                       return "未知的系统命令";
        case TEMPERATURE:               return "未知的温控命令";
        case NFC:                       return "未知的NFC命令";
        case GYRO:                      return "未知的GYRO命令";
        case ZAXIS:                     return "未知的轴命令";
        case COVER_AXIS:                return "未知的COVER_AXIS命令";
        case LIGHT_STRIP:               return "未知的灯带命令";
        case PCU_MOD:                   return "未知的PCU_MOD命令";
        }
    }

    return "未知的其他命令";
}
```

```
using ByteArray = std::vector<uint8_t>;
```



```
ByteArray GenRawCmd(uint16_t seq, uint8_t frameType,
                    uint8_t deviceType, uint8_t deviceFunc,
                    uint8_t state, const ByteArray &data)
{
    ByteArray outbuf;
    outbuf.reserve(64);
    heygears::DataStream stream(&outbuf);
    stream.setByteOrder(heygears::DataStream::BigEndian);
    stream << PROTOCOL_HEAD
           << PROTOCOL_VERSION
           << static_cast<uint8_t>(data.size() + PRE_SEGMENT_SIZE)
           << frameType
           << seq
           << deviceType
           << deviceFunc
           << state;

    outbuf.insert(outbuf.end(), data.begin(), data.end());

    stream << CrcCode::Crc16ForModbus(outbuf)
           << PROTOCOL_TAIL;

    return outbuf;
}
```



对seq的处理

```
bool ret = ptr->waitForResult(seq);
```



```
bool SlaveModule::waitForResult(int seq)
{
    return mDevice->waitForResult(seq);
}
```



```
bool DeviceMsgMgr::waitForResult(uint16_t seq)
{
    std::unique_lock<std::mutex> lock(mMsgMapLock);
    auto iter = mMsgMap.find(seq);
    if(iter == mMsgMap.end())
    {
        warning() << "消息不在列表中, seq:" << std::hex << seq;
        return true;
    }

    auto msg = iter->second;
    lock.unlock();

    return waitForResult(msg);
}
```



```
bool DeviceMsgMgr::waitForResult(const DeviceMsgPtr &msg)
{
    if(!waitForAck(msg))
    {
        warning() << "等待ack返回失败, " << msg->mReqMessage;
        return false;
    }

    if(!msg->mNeedResult)
    {
        info() << "该消息不需要结果返回";
        return true;
    }

    while(!msg->mAlreadyResultTimeout)
    {
        if(msg->mAlreadyResult)
            return true;

        processEvent();
    }

    // 在超时后做最后一次检查，避免消息队列繁忙导致的假超时
    if(msg->mAlreadyResult)
        return true;

    return false;
}
```



```
bool DeviceMsgMgr::waitForAck(const DeviceMsgPtr &msg)
{
    if(!msg->mNeedAck)
    {
        info() << "该消息不需要ack应答";
        return true;
    }

    while(!msg->mAlreadyAckTimeout)
    {
        if(msg->mAlreadyAck)
            return true;

        processEvent();
    }

    // 在超时后做最后一次检查，避免消息队列繁忙导致的假超时
    if(msg->mAlreadyAck)
        return true;

    return false;
}
```

