alpaca

创建类

```
class REST(object):
    def __init__(self,
                 key_id: str = None,
                 secret_key: str = None,
                 base_url: URL = None,
                 api_version: str = None,
                 oauth=None,
                 raw_data: bool = False
                 ):
        """
        :param raw_data: should we return api response raw or wrap it with
                         Entity objects.
        """
        self._key_id, self._secret_key, self._oauth = get_credentials(
            key_id, secret_key, oauth)
        self._base_url: URL = URL(base_url or get_base_url())
        self._api_version = get_api_version(api_version)
        self._session = requests.Session()
        self._use_raw_data = raw_data
        self._retry = int(os.environ.get('APCA_RETRY_MAX', 3))
        self._retry_wait = int(os.environ.get('APCA_RETRY_WAIT', 3))
        self._retry_codes = [int(o) for o in os.environ.get(
            'APCA_RETRY_CODES', '429,504').split(',')]

```

