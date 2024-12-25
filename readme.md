# gphotos_mobile_client

Very basic, reverse engineered, Google Photos mobile API client.  
Made for uploading files as Pixel XL without running an emulator.

---

### Set Up

```
pip install -r requirements.txt
```

### Example Usage

```python
from gphotos_mobile_client import GPhotosMobileClient

file_path = "/path/to/media_file.jpg"
auth_data = "androidId=216e583113f43c75&app=com.google.android.apps.photos&client_sig=34bb24c05e47e0aefa65a58a762171d9b613a680..."


client = GPhotosMobileClient(auth_data=auth_data)
media_key = client.upload_file(file_path=file_path, progress=True)
print(media_key)

```

CLI

```
usage: gphotos_mobile_client.py [-h] [--progress] [--force-upload] file_path auth

Google Photos mobile client.

positional arguments:
  file_path       Path to the file to upload.
  auth            Google auth data for authentication.

options:
  -h, --help      show this help message and exit
  --progress      Display upload progress.
  --force-upload  Upload the file even if it is already uploaded.
```

### Auth data? Where do i get mine?

Below is a step by step instruction on how to accuire your Google account's mobile auth data in a simplest way possible.

1. Get a rooted android device or an emulator.
2. Connect the device to your PC via ADB.
3. Install https://httptoolkit.com
4. In HTTP Toolkit, select Intercept - Android Device via ADB. Filter traffic with `contains(https://www.googleapis.com/auth/photos.native)`
5. Open Google Photos app and login with your account.
6. There should be a single request found.
   If you're not seeing it, delete the google account from the device and log in again.  
   Copy request body data as text.  
    ![http_toolkit_tip](media/image.png)
7. Now you've got yourself your auth data! 🎉

### My Other Google Photos scripts and tools

- https://github.com/xob0t/gp-file-hide
- https://github.com/xob0t/Google-Photos-Toolkit
