# minio-async
> Asynchronous MinIO Python Client API

## Declaration
This project is based on Huseyn Mashadiyev's [minio-async](https://github.com/HuseynMashadiyev/minio-async/tree/78128443f7ce9618191e1155689b47507df67bb1) 1.0.0

The modification is from my [miniopy-async](https://github.com/hlf20010508/miniopy-async/tree/3fb12756d1f3822bf91a368219061a8519fd8372) 1.2

<br/>

## Dependencies
- Python>3.6

<br/>

## Build from source
```sh
git clone https://github.com/hlf20010508/minio-async.git
cd minio-async
python setup.py install
```

<br/>

## Install with pip

PyPI
```sh
pip install minio-async
```

Github Repository
```sh
pip install git+https://github.com/hlf20010508/minio-async.git
```

<br/>

## Install with pipenv

PyPI
```sh
pipenv install minio-async
```

Github Repository
```sh
pipenv install git+https://github.com/hlf20010508/minio-async.git#egg=minio-async
```

<br/>

## Usage
```python
import minio_async
```

### Examples
```python
from minio_async import Minio
import asyncio

client = Minio(
    "play.min.io",
    access_key="Q3AM3UQ867SPQQA43P2F",
    secret_key="zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG",
    secure=True  # http for False, https for True
)

async def main():
    url = await client.presigned_get_object("my-bucket", "my-object")
    print('url:', url)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
loop.close()
```

```python
from sanic import Sanic
from minio_async import Minio

app = Sanic(__name__)

client = Minio(
    "play.min.io",
    access_key="Q3AM3UQ867SPQQA43P2F",
    secret_key="zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG",
    secure=True  # http for False, https for True
)

@app.route('/download', methods=['GET'])
async def download(request):
    print('downloading ...')
    bucket=request.form.get('bucket')
    fileName=request.form.get('fileName')

    # decodeURI, for those which has other language in fileName, such as Chinese, Japanese, Korean
    fileName = parse.unquote(fileName)

    url = await client.presigned_get_object(bucket_name=bucket, object_name=fileName)
    return redirect(url)
```

Check more examples in <a href="https://github.com/hlf20010508/minio-async/tree/master/examples">examples</a>

Refer documents in <a href="https://github.com/hlf20010508/minio-async/tree/master/docs">docs</a>

<br/>

## Link
- <a href="https://pypi.org/project/minio-async/">minio-async</a> on PyPI
- <a href="https://github.com/hlf20010508/minio-async.git">minio-async</a> on Github
