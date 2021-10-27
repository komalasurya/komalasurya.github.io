# My Photos
My Photos is an android application to store photo in cloud for free and safe. You could find it too on [github](https://github.com/komalasurya/komalasurya.github.io/blob/main/Case.md)

# Screen

## Login
![Login](https://lh3.googleusercontent.com/pw/AM-JKLVgRCpuJIpPrR_gy3utBQag4VMCMPvSMcmhG_hvGuoRhnOthhLkIYryPcqwx8R7QXerl3K2lHCLQW_SdcVRJCUQN6D77CPCXz4VSZCitqoPelHyzmClQShoY7f6YDc_lXPCcnN-0YmJGgwKj1JUv7kK=w321-h649-no)

Use appropriate input type for each fields. Save access token from [Login API](###Login) for uploading report in report page. Show error message if [Login API](###Login) returns error. Save access token from [Login API](###Login) for all API endpoints.  Redirect to login page whenever the access token is expired or API request fails with unauthorized (http status code 401). Show errors from API whenever login request isn't succeed.

## Register
![Register](https://lh3.googleusercontent.com/pw/AM-JKLVpxD4LiHezSxxKtsbBfv-WQ4Y0fCj9IhrpUkSE_4D-UnC8fSA7Y1P8lKtKx3ftJcbBc52eP-SgCJFYktcYF0YVx8xj3SnF35ipK2JJkmk6ftttSl-A720Qx6TbXXaAqhvv9toTcrPTiv-AH4aeHED9=w322-h649-no)

You can access this menu by click register button on [Login Page](##Login). Use appropriate input type for each fields. User should have password length must be greater than 8 and mixes of lowercase & uppercase characters, numeric & symbols and must match with confirm password field. Show errors from API whenever login request isn't succeed


## Homescreen
![Homescreen](https://lh3.googleusercontent.com/pw/AM-JKLWu6lJr5KuEUNA8YzHbUVeF1mltYGvJ5cecktfNT6t75_U3ki5VlafZ_0z3YwnTaBOFNp5-50TfWAWVglXvyL3cOWj4sE6h5QQ_TPx6TscjugeTYEPYrnlixnzU9sYEHLgQ22H8LhbweEdAH0zc7pC7=w348-h649-no)

You can access this page after login or user has logged in before. Page divided into 2 parts, the first one is album list, second one is photos list. Show and animate `upload photo` & `create album` button whenever `+` floating button clicked by user.
![Button Animation](https://lh3.googleusercontent.com/pw/AM-JKLWfUlWJNyG0FncFfONXGYah2orxyWz3IChBs5YarQQ5eiy9fKxIl3rCS3RfxHhlovbSKOTv8m9lILm9qcPiDFGnoCoMzTS8D8o5MqPMVY6k8r_neW_Q_lokL36s4gkJM5IJJAMP7N0-f1YVZnxTHjVq=w623-h1314-no)

### Album list
Get album list from [Album List API](###AlbumList) Show folder icon and album name beside it.

### Photo List
Get photo list from [Photo List API](###PhotoList) and show it in grid with 2 columns. Show photo above the name. Show loading icon before image loaded. Load image from internet shouldn't block users from doing anything

## Create Album
![CreateAlbum](https://lh3.googleusercontent.com/pw/AM-JKLVddRicVTAdDUmSbApvvJOMmkAxvSncmZHLpDgwulQMDLKtqh1yxqBiDlsGyUiU0rMSpA49RfV7CIxL34co1_kUa4Tf4keT79QBmmwJBENU_UuasePBpxaYuJRQpFF2YqvW2ornZrIiX1DUYcoEaGdn=w351-h650-no)

Show dialog to input album name. Call [Create Album API](###CreateAlbum) when user click button `create`. Navigate users to album page when album successfully created

## Upload Photo
![Upload Photo](https://lh3.googleusercontent.com/pw/AM-JKLUe9N3mPKEAtz1xDNCyrBRw6rly_P3UiDlhfV9cxy8ujBHH9-Eoq6zSOWIDpR5Ha5-92MLcG9N0HO_VByvHC6QF6PcBK5yVltYxoWRMHoDvYxj6XGq-A9_uR1BXTb4vC9PtwQ1xTXLWenNWw4T9VDVN=w322-h649-no)

User can access this page after click upload photo on floating button. Show name inside the page. User can choose photo and upload it to [Upload Photo API](###UploadPhoto)

## Album
![Album](https://lh3.googleusercontent.com/pw/AM-JKLXbSPaJP5pntqLWh6YeqQB80NvmVzGWMJlQ093rsM-HgdA13THtCzYTwxPLYE1eP0kEY2UCNyVNRqCjyFugEkQiiPc2N-WQ1gHD2-xLjjZIwsKpEwEjc5VHXRPo5TI0r3_F93NgF8E0zzC4R3m1f_lO=w348-h649-no)

You can access this page by click on one of the albums on the homescreen. Show album name above photo list. Download image to device when user click to one of the photo in the list.

# API
Use this host for all endpoints
```
http://54.151.137.160/api/v1
```

## Auth
### Login
- Path: `/auth`
- Method: `POST`
- Request Body:
  1. email
  2. password
- Heades:
  1. `Accept` = `application/json`
  2. `Content-Type` = `application/json`
- Response:
  1. signature
  2. expires_in - signature valid time countdown
 
  Sample:
  - Request:
  ```curl
  curl -X POST \
    http://54.151.137.160/api/v1/auth \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    -H 'cache-control: no-cache' \
    -d '{
        "email":"komala.surya.w@gmail.com",
        "password":"secret"
    }'
  ```
  - Response:
  ```json
    {
        "data": {
            "expires_in": 3600,
            "signature": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJkNjY1M2NhMS05OGJlLTQwNjItODViZC01ZTRmNmVjMWRkMTkiLCJ1c2VybmFtZSI6ImtvbWFsYXN1cnlhMiIsImV4cCI6MTYwMjk5NzkwMX0.qsZNZ0Z5GWqVHzlKmTrrIrk8a7Ik2bBzMwDqzSZShKU9OBsI5B5gENn4_Xinh0Hq9NqZckSJYtd0M3cHfjtcLQ"
        },
        "meta": {
            "version": "1",
            "hostname": "Komalas-MacBook-Pro.local",
            "client_ip": "127.0.0.1"
        }
    }
  ```
  
### Register
- Path: `/users`
- Method: `POST`
- Request Body:
  1. username
  2. Email
  3. password
- Heades:
  1. `Accept` = `application/json`
  2. `Content-Type` = `application/json`    
 
  Sample:
  - Request:
  ```curl
  curl -X POST \
    http://54.151.137.160/api/v1/users \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    -H 'cache-control: no-cache' \
    -d '{
        "name":"komalasurya2",
        "email": "komalasurya1@gmail.com",
        "password":"secret1"
    }'
  ```
  - Response:
  ```json
    {
        "data": {
            "username": "komalasurya",
            "email": "komalasurya@gmail.com",
            "password": "$2y$10$kRxB0N.xsW3OS/aRfV0DVuFVFdOpvBuBaKWZPJpcSnHxwLv1XCLXi",
            "id": "011b1ceb-30dd-4777-87c9-b41b204988f4",
            "updated_at": "2020-10-18 06:17:10",
            "created_at": "2020-10-18 06:17:10"
        },
        "meta": {
            "version": "1",
            "hostname": "Komalas-MacBook-Pro.local",
            "client_ip": "127.0.0.1"
        }
    }
  ```

### Get Users
- Path: `/users/me`
- Method: `GET`
- Heades:
  1. `Accept` = `application/json`
  2. `Content-Type` = `application/json`   
  3. `Authorization` = `bearer {access_token}` 
- Response (array):
  1. id
  2. name
  3. email
 
  Sample:
  - Request:
  ```curl
  curl -X POST \
    http://54.151.137.160/api/v1/users/me \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    -H 'cache-control: no-cache' \
    -H `Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJlM2UzYzMwOS1iNGMyLTQ5ZWEtOGZhZi04NGJlZTc1MTU0MmIiLCJleHAiOjE2MzUxMjY2NDl9.xvDBRIYnVWFAAux9ACLY7e4BNQ-wy8B5C_f1oWCVC-rchv84ww_b9ssDr_tIroD_LTGNxp9xbGd7fKYk-SfVpQ`
  ```
  - Response:
  ```json
    {
        "data": {
            "id": "e3e3c309-b4c2-49ea-8faf-84bee751542b",
            "name": "komala surya",
            "email": "komala.surya.w@gmail.com",
            "remember_token": null,
            "created_at": "2021-10-22T15:38:29.000000Z",
            "updated_at": "2021-10-22T15:38:29.000000Z"
        },
        "meta": {
            "version": "1",
            "hostname": "komala-surya",
            "client_ip": "127.0.0.1"
        }
    }
  ```

## Album
### AlbumList
- Path: `/users/{user_id}/albums`
- Method: `GET`
- Headers:
  1. `Accept` = `application/json`
  2. `Authorization` = `bearer {access_token}` 
- Response (array):
  1. id
  2. name

  Sample:
  - Request:
  ```curl
  curl -X POST \
    http://54.151.137.160/api/v1/users/e3e3c309-b4c2-49ea-8faf-84bee751542b/albums \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    -H 'cache-control: no-cache' \
    -H `Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJlM2UzYzMwOS1iNGMyLTQ5ZWEtOGZhZi04NGJlZTc1MTU0MmIiLCJleHAiOjE2MzUxMjY2NDl9.xvDBRIYnVWFAAux9ACLY7e4BNQ-wy8B5C_f1oWCVC-rchv84ww_b9ssDr_tIroD_LTGNxp9xbGd7fKYk-SfVpQ`
  ```
  - Response:
  ```json
    {
        "data": [{
            "id": "f7a167eb-4f48-490b-ad6e-5ce99f8d7f6f",
            "user_id": "e3e3c309-b4c2-49ea-8faf-84bee751542b",
            "name": "hello world",
            "created_at": "2021-10-22T15:39:02.000000Z",
            "updated_at": "2021-10-22T15:39:02.000000Z"
        }],
        "meta": {
            "pagination": {
                "current_page": 1,
                "from": 1,
                "last_page": 1,
                "links": [
                    {
                        "url": null,
                        "label": "&laquo; Previous",
                        "active": false
                    },
                    {
                        "url": "http://54.151.137.160/api/v1/users/e3e3c309-b4c2-49ea-8faf-84bee751542b/albums?page=1",
                        "label": "1",
                        "active": true
                    },
                    {
                        "url": null,
                        "label": "Next &raquo;",
                        "active": false
                    }
                ],
                "path": "http://54.151.137.160/api/v1/users/e3e3c309-b4c2-49ea-8faf-84bee751542b/albums",
                "per_page": 50,
                "to": 1,
                "total": 1
            },
            "version": "1",
            "hostname": "komala-surya",
            "client_ip": "127.0.0.1"
        }
    }
  ```

### CreateAlbum
- Path: `/albums`
- Method: `POST`
- Request Body:
  1. name
- Heades:
  1. `Accept` = `application/json`
  2. `Content-Type` = `application/json`    
- Response:
  1. id
  2. name
  3. user
 
  Sample:
  - Request:
  ```curl
  curl -X POST \
    http://54.151.137.160/api/v1/albums \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    -H 'cache-control: no-cache' \
    -d '{
        "name":"hello"
    }'
  ```
  - Response:
  ```json
    {
        "data": {
            "user": {
                "id": "e3e3c309-b4c2-49ea-8faf-84bee751542b",
                "name": "komala surya",
                "email": "komala.surya.w@gmail.com",
                "remember_token": null,
                "created_at": "2021-10-22T15:38:29.000000Z",
                "updated_at": "2021-10-22T15:38:29.000000Z"
            },
            "name": "hello world",
            "user_id": "e3e3c309-b4c2-49ea-8faf-84bee751542b",
            "id": "618a2d11-74b8-4752-b427-bfad51900bdc",
            "updated_at": "2021-10-25T16:45:52.000000Z",
            "created_at": "2021-10-25T16:45:52.000000Z"
        },
        "meta": {
            "version": "1",
            "hostname": "Komalas-MacBook-Pro.local",
            "client_ip": "127.0.0.1"
        }
    }
  ```
 
## Photo

### PhotoList
- Path: `/users/{user_id}/photos`
- Method: `GET`
- Params:
  1. album (opt) - album id
- Headers:
  1. `Accept` = `application/json`
  2. `Authorization` = `bearer {access_token}` 
- Response (array):
  1. id
  2. album
  3. name
  4. size (in bytes)
  5. created_at, updated_at (timestamp)
  6. image

  Sample:
  - Request:
  ```curl
  curl -X POST \
    http://54.151.137.160/api/v1/users/e3e3c309-b4c2-49ea-8faf-84bee751542b/albums \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    -H 'cache-control: no-cache' \
    -H `Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJlM2UzYzMwOS1iNGMyLTQ5ZWEtOGZhZi04NGJlZTc1MTU0MmIiLCJleHAiOjE2MzUxMjY2NDl9.xvDBRIYnVWFAAux9ACLY7e4BNQ-wy8B5C_f1oWCVC-rchv84ww_b9ssDr_tIroD_LTGNxp9xbGd7fKYk-SfVpQ`
  ```
  - Response:
  ```json
    {
        "data": [{
            "album": {
                "id": "f7a167eb-4f48-490b-ad6e-5ce99f8d7f6f",
                "user_id": "e3e3c309-b4c2-49ea-8faf-84bee751542b",
                "name": "hello world",
                "created_at": "2021-10-22T15:39:02.000000Z",
                "updated_at": "2021-10-22T15:39:02.000000Z"
            },
            "id": "51c4f54f-ff81-45c6-b105-74160d2de2ac",
            "user_id": "e3e3c309-b4c2-49ea-8faf-84bee751542b",
            "album_id": "f7a167eb-4f48-490b-ad6e-5ce99f8d7f6f",
            "name": "bbb-splash.png",
            "size": 1527631,
            "created_at": "2021-10-22T15:51:16.000000Z",
            "updated_at": "2021-10-22T15:51:16.000000Z",
            "image": "http://54.151.137.160/api/v1/photos/51c4f54f-ff81-45c6-b105-74160d2de2ac/image"
        }],
        "meta": {
            "pagination": {
                "current_page": 1,
                "from": 1,
                "last_page": 1,
                "links": [
                    {
                        "url": null,
                        "label": "&laquo; Previous",
                        "active": false
                    },
                    {
                        "url": "http://54.151.137.160/api/v1/users/e3e3c309-b4c2-49ea-8faf-84bee751542b/photos?page=1",
                        "label": "1",
                        "active": true
                    },
                    {
                        "url": null,
                        "label": "Next &raquo;",
                        "active": false
                    }
                ],
                "path": "http://54.151.137.160/api/v1/users/e3e3c309-b4c2-49ea-8faf-84bee751542b/photos",
                "per_page": 50,
                "to": 1,
                "total": 1
            },
            "version": "1",
            "hostname": "komala-surya",
            "client_ip": "127.0.0.1"
        }
    }
  ```

### UploadPhoto
- Path: `/photos`
- Method: `POST`
- Request Body:
  1. album - album id
  2. image - file
- Heades:
  1. `Accept` = `application/json`
  2. `Content-Type` = `application/json`    
 
  Sample:
  - Request:
  ```curl
  curl -X POST \
    http://54.151.137.160/api/v1/photos \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    -H 'cache-control: no-cache' \
    -H `Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJlM2UzYzMwOS1iNGMyLTQ5ZWEtOGZhZi04NGJlZTc1MTU0MmIiLCJleHAiOjE2MzUxMjY2NDl9.xvDBRIYnVWFAAux9ACLY7e4BNQ-wy8B5C_f1oWCVC-rchv84ww_b9ssDr_tIroD_LTGNxp9xbGd7fKYk-SfVpQ` \
    --form 'album="f7a167eb-4f48-490b-ad6e-5ce99f8d7f6f"' \
    --form 'image=@"/Users/komalasurya/Downloads/bbb-splash.png"'
  ```
  - Response:
  ```json
    {
        "data": {
            "user": {
                "id": "e3e3c309-b4c2-49ea-8faf-84bee751542b",
                "name": "komala surya",
                "email": "komala.surya.w@gmail.com",
                "remember_token": null,
                "created_at": "2021-10-22T15:38:29.000000Z",
                "updated_at": "2021-10-22T15:38:29.000000Z"
            },
            "album": {
                "id": "f7a167eb-4f48-490b-ad6e-5ce99f8d7f6f",
                "user_id": "e3e3c309-b4c2-49ea-8faf-84bee751542b",
                "name": "hello world",
                "created_at": "2021-10-22T15:39:02.000000Z",
                "updated_at": "2021-10-22T15:39:02.000000Z"
            },
            "size": 67376,
            "name": "google.jpg",
            "id": "9d70fb82-43e0-49d8-8d6d-6ef29ea99f31",
            "user_id": "e3e3c309-b4c2-49ea-8faf-84bee751542b",
            "album_id": "f7a167eb-4f48-490b-ad6e-5ce99f8d7f6f",
            "updated_at": "2021-10-25T16:35:47.000000Z",
            "created_at": "2021-10-25T16:35:47.000000Z",
            "image": "http://54.151.137.160/api/v1/photos/9d70fb82-43e0-49d8-8d6d-6ef29ea99f31/image"
        },
        "meta": {
            "version": "1",
            "hostname": "Komalas-MacBook-Pro.local",
            "client_ip": "127.0.0.1"
        }
    }
  ```

## Postman Link
[Postman collection](https://www.getpostman.com/collections/ebfc341a9cfeb75412db)