<h1 align="center">Yemek Tarifleri API</h1>

<div align=center>
  <img src="./Readme%20Resources/Yemek Tarifleri API Logo.png" alt="Logo" width="120" heigh="120"/>
</div>

## **İçindekiler**

- [API Hakkında](#api-hakkında)
- [Dokümantasyon](#dokümantasyon)
  - [GET İsteği](#get-i̇steği)
  - [POST İsteği](#post-i̇steği)
  - [PUT İsteği](#put-i̇steği)
  - [DELETE İsteği](#delete-i̇steği)
- [İstek Örnekleri](#i̇stek-örnekleri)
  - [GET Örnekleri](#get-örnekleri)
  - [POST Örnekleri](#post-örnekleri)
  - [PUT Örnekleri](#put-örnekleri)
  - [DELETE Örnekleri](#delete-örnekleri)
- [Lisans](#lisans)
- [İletişim](#i̇letişim)


![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)

<a href="https://github.com/mustafatoktas/W.BE_RepoVisitorCounterAPI" target="_blank"> <img src="https://toktasoft.com/api/github/repo-visitor-counter.php?repo=hnq3dyszavc69re&show_repo_name=1&show_date=1&show_brand=0" alt="Repo Visitor Counter API"/> </a>


![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)

## API Hakkında

Bu repo, PHP diliyle geliştirmiş olduğum yemek tariflerini sunan API'nin dokümantasyonunu içerir.

Bu API, yemek tariflerini ekleme, güncelleme, silme ve listeleme işlemleri yapmaya olanak tanır.

Tarifler, tarifin eklenme tarihi ve ekleyen API anahtarı kaydedilir.
Ayrıca tarif ekleme ve güncelleme isteklerinde karakter sayısı denetlenir. 

`title` için maksimum 60 karakter

`ingredients` için maksimum 300 karakter

`instructions` için maksimum 1200 karakter

API anahtarları aylık maksimum 100 istek ile sınırlandırılmıştır. API anahtarı sahibi olabilmek
veya ayrıcalıklı kullanıcı statüsüne geçip sınırsız istek hakkına sahip olabilmek için iletişime geçilmesi gerekilmektedir.


![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)

## Dokümantasyon

Base URL: `https://toktasoft.com/api/recipes.php`

API, dört ana işlevi yerine getiren `GET`, `POST`, `PUT` ve `DELETE` türündeki HTTP isteklerini destekler.

### GET İsteği

| Parametre                       | Zorunlu Mu?                 | Açıklama                                                          |
| ------------------------------- | --------------------------- | ----------------------------------------------------------------- |  
| <p align="center">`api_key`</p> | <p align="center">evet</p>  | Geçerli bir API anahtarı.                                         |
| <p align="center">`id`</p>      | <p align="center">hayır</p> | Belirli bir tarifin ID'si. Belirtilmezse tüm tarifler listelenir. |

### POST İsteği

Yeni tarif eklemek için kullanılır.

| Parametre                       | Zorunlu Mu?                | Açıklama                  |
| ------------------------------- | -------------------------- | ------------------------- |
| <p align="center">`api_key`</p> | <p align="center">evet</p> | Geçerli bir API anahtarı. |

Gönderilen JSON formatındaki veriler:

```json
{
  "title": "Tarifin başlığı",
  "ingredients": "Tarifin malzemeleri",
  "instructions": "Tarifin yapılış talimatları"
}
```

### PUT İsteği

Mevcut bir tarifi güncellemek için kullanılır.

| Parametre                       | Zorunlu Mu?                | Açıklama                     |
| ------------------------------- | -------------------------- | ---------------------------- |
| <p align="center">`api_key`</p> | <p align="center">evet</p> | Geçerli bir API anahtarı.    |

Gönderilen JSON formatındaki veriler:

```json
{
  "id": 1,
  "title": "Yeni başlık",
  "ingredients": "Yeni malzemeler",
  "instructions": "Yeni yapılış talimatları"
}
```

### DELETE İsteği

Mevcut bir tarifi silmek için kullanılır.

| Parametre                       | Zorunlu Mu?                | Açıklama                  |
| ------------------------------- | -------------------------- | ------------------------- |
| <p align="center">`api_key`</p> | <p align="center">evet</p> | Geçerli bir API anahtarı. |
| <p align="center">`id`</p>      | <p align="center">evet</p> | Silinecek tarifin ID'si.  |


![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)

## İstek Örnekleri

İstek örnekleri curl komut satırı aracı kullanılarak gösterilmiştir.

### GET Örnekleri

✅**Bütün yemek tarifleri**

```sh
curl -X GET "http://toktasoft/api/recipes.php?api_key=myapikey"
```

```json
{
    "success": true,
    "result": [
        {
            "id": "1",
            "title": "Spaghetti",
            "ingredients": "Makarna, Domates Sosu, Peynir",
            "instructions": "Makarnayı haşlayın, sosu ekleyin ve peynirle servis edin.",
            "created_at": "2024-07-11 08:04:14",
            "updated_at": "2024-07-11 08:04:14"
        },
        {
            "id": "2",
            "title": "Salata",
            "ingredients": "Marul, Domates, Salatalık, Zeytinyağı, Limon",
            "instructions": "Tüm malzemeleri doğrayın ve karıştırın.",
            "created_at": "2024-07-11 13:16:21",
            "updated_at": "2024-07-11 19:34:47"
        }
    ],
    "monthly_request_count": 52
}
```

✅**Belirli bir yemek tarifi**

```sh
curl -X GET "http://toktasoft/api/recipes.php?api_key=myapikey&id=1"
```

```json
{
    "success": true,
    "result": {
        "id": 1,
        "title": "Spaghetti",
        "ingredients": "Makarna, Domates Sosu, Peynir",
        "instructions": "Makarnayı haşlayın, sosu ekleyin ve peynirle servis edin.",
        "created_at": "2024-07-11 08:04:14",
        "updated_at": "2024-07-11 08:04:14"
    },
    "monthly_request_count": 68
}
```

❌**Belirli bir yemek tarifi**

Olmayan bir yemek tarifi için istek atıldığında hata döndürülür.

```sh
curl -X GET "http://toktasoft/api/recipes.php?api_key=myapikey&id=100"
```

```json
{
    "success": false,
    "error": "Tarif bulunamadı.",
    "monthly_request_count": 102
}
```

❌**Belirli bir yemek tarifi**

Aylık istek sınırına ulaşılmışsa hata döndürülür.

```sh
curl -X GET "http://toktasoft/api/recipes.php?api_key=myapikey&id=1"
```

```json
{
    "success": false,
    "error": "Aylık istek sınırına ulaşıldı.",
    "monthly_request_count": 100
}
```

### POST Örnekleri

✅**Yeni bir yemek tarifi ekleme**

```sh
curl -X POST "https://toktasoft.com/api/recipes.php?api_key=myapikey" -H "Content-Type: application/json" -d '{
  "title": "Omlet",
  "ingredients": "Yumurta, Tuz, Karabiber",
  "instructions": "Yumurtaları çırpın, tuz ve karabiber ekleyin, tavada pişirin."
}'
```

```json
{
  "success": true,
  "message": "Yemek tarifi başarıyla eklendi.",
  "monthly_request_count": 92
}
```

❌**Yeni bir yemek tarifi ekleme**

Alanlar boş bırakılırsa yada eksik gönderilirse hata döndürülür.

```sh
curl -X POST "https://toktasoft.com/api/recipes.php?api_key=myapikey" -H "Content-Type: application/json" -d '{
  "title": "",
  "ingredients": "Yumurta, Tuz, Karabiber",
  "instructions": "Yumurtaları çırpın, tuz ve karabiber ekleyin, tavada pişirin."
}'
```

```json
{
    "success": false,
    "error": "Eksik veya boş parametreler.",
    "monthly_request_count": 304
}
```

### PUT Örnekleri

✅**Mevcut bir yemek tarifini güncelleme**

```sh
curl -X PUT "https://toktasoft.com/api/recipes.php?api_key=myapikey" -H "Content-Type: application/json" -d '{
  "id": 1,
  "title": "Güncellenmiş Spaghetti",
  "ingredients": "Makarna, Domates Sosu, Peynir",
  "instructions": "Makarnayı haşlayın, sosu ekleyin ve peynirle servis edin."
}'
```

```json
{
  "success": true,
  "message": "Yemek tarifi başarıyla güncellendi.",
  "monthly_request_count": 107
}
```

❌**Mevcut bir yemek tarifini güncelleme**

Olmayan yada bir yemek tarifi güncellenmeye çalışılırsa hata döndürülür.

```sh
curl -X PUT "https://toktasoft.com/api/recipes.php?api_key=myapikey" -H "Content-Type: application/json" -d '{
  "id": 999,
  "title": "Güncellenmiş Spaghetti",
  "ingredients": "Makarna, Domates Sosu, Peynir",
  "instructions": "Makarnayı haşlayın, sosu ekleyin ve peynirle servis edin."
}'
```

```json
{
    "success": false,
    "error": "Böyle bir tarif bulunamadı.",
    "monthly_request_count": 60
}
```

❌**Mevcut bir yemek tarifini güncelleme**

Güncellenmek istenen yemek tarifinin ilgili alanları boş bırakılırsa yada
eksik gönderilirse hata döndürülür.

```sh
curl -X PUT "https://toktasoft.com/api/recipes.php?api_key=myapikey" -H "Content-Type: application/json" -d '{
  "id": 1,
  "title": "Güncellenmiş Spaghetti",
  "ingredients": "Makarna, Domates Sosu, Peynir"
}'
```

```json
{
    "success": false,
    "error": "Eksik veya boş parametreler.",
    "monthly_request_count": 341
}
```

### DELETE Örnekleri

✅**Mevcut bir yemek tarifini silme:**

```sh
curl -X DELETE "https://toktasoft.com/recipes.php?api_key=myapikey&id=1"
```

```json
{
  "success": true,
  "message": "Yemek tarifi başarıyla silindi.",
  "monthly_request_count": 207
}
```


![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)

## Lisans
    Copyright 2024 Mustafa TOKTAŞ

    Licensed under the GNU General Public License v3.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        https://www.gnu.org/licenses/gpl-3.0.html

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.


![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)

## İletişim

<a href="mailto:info@mustafatoktas.com"              target="_blank"> <img src="./Readme Resources/İletişim/Mail.png"     alt="Mail"     width="64" heigh="64"/> </a>
<a href="https://t.me/mustafatoktas00"               target="_blank"> <img src="./Readme Resources/İletişim/Telegram.png" alt="Telegram" width="64" heigh="64"/> </a>
<a href="https://www.linkedin.com/in/mustafatoktas/" target="_blank"> <img src="./Readme Resources/İletişim/LinkedIn.png" alt="LinkedIn" width="64" heigh="64"/> </a>