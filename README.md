# Zillow Scraper

[![Promo](https://github.com/bright-kr/LinkedIn-Scraper/blob/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.co.kr/products/web-scraper/zillow) 

이 리포지토리는 Zillow 데이터를 スクレイピング하기 위한 두 가지 서로 다른 방법을 제공합니다:
1. 기본적인 데이터 수집을 위한 무료 소규모 스크레이퍼
2. 대규모 데이터 추출을 위한 엔터프라이즈급 API 솔루션

## Table of Contents
- [Free Zillow Data Scraper](#free-zillow-data-scraper)
- [Limitations of Free Scraper](#limitations-of-free-scraper)
- [Zillow Scraper API](#zillow-scraper-api)
  - [Key Features](#key-features)
  - [Quick Start Guide](#quick-start-guide)
  - [Zillow Property Details by URL](#1-zillow-property-details-by-url)
  - [Zillow Properties Listing by Filters](#2-zillow-properties-listing-by-filters)
  - [Zillow Properties Listing by URL](#3-zillow-properties-listing-by-url)
  - [Zillow Price History](#4-zillow-price-history)
- [No-Code Scraper Option](#no-code-scraper-option)
- [Additional Options](#additional-options)
- [Support & Resources](#support--resources)

## Free Zillow Data Scraper
무료 스크레이퍼를 사용하면 소규모로 Zillow 검색 페이지에서 부동산 데이터를 수집할 수 있습니다.

### Input Requirements
| Parameter | Required | Description |
|-----------|----------|-------------|
| coords    | Yes      | 경계 좌표 [west, east, south, north] |
| pages     | Yes      | スクレイピング할 페이지 수 |

### Implementation
스크레이퍼를 사용하려면, 위치와 데이터 요구사항에 맞게 아래 코드에서 좌표와 페이지 수를 수정하십시오:
```python
# free_zillow_scraper/property_data.py
def get_search_params():
    return (
        -118.668176,  # West longitude
        -118.155289,  # East longitude
        33.703652,    # South latitude
        34.337306,    # North latitude
        5             # Number of pages to scrape
    )
```

**힌트:** 지리 좌표는 어떤 위치든 Zillow 검색 페이지의 `<script>` 태그에서 찾을 수 있습니다. 다음 태그를 확인하십시오:
```bash
<script id="__NEXT_DATA__" type="application/json">
```

### Sample Output
```json
{
    "id": "20595672",
    "price": "$1,599,900",
    "zestimate": 1605500,
    "location": {
        "address": "2215 Wellington Rd, Los Angeles, CA 90016",
        "city": "Los Angeles",
        "state": "CA",
        "zip": "90016",
        "coordinates": {"lat": 34.036064, "lon": -118.33622},
    },
    "details": {
        "beds": 4,
        "baths": 3.0,
        "area_sqft": 1886,
        "lot_acres": 8577.0,
        "property_type": "SINGLE_FAMILY",
    },
    "listing": {
        "status": "House for sale",
        "days_on_zillow": 5,
        "broker": "ehomes",
        "url": "https://www.zillow.com/homedetails/2215-Wellington-Rd-Los-Angeles-CA-90016/20595672_zpid/",
    },
},
```

## Limitations of Free Scraper
무료 Zillow 스크레이퍼는 소규모 데이터 추출에는 잘 작동하지만, 다음과 같은 제한이 있습니다:

- **レート制限:** 몇 차례 スクレイピング 후 Zillow가 리クエスト를 차단합니다.
- **IPアドレス 차단:** 동일한 IP아ドレス에서 빈번히 スクレイピング하면 차단(밴)될 수 있습니다.
- **제한된 확장성:** 대용량 데이터 수집에는 적합하지 않습니다.
- **CAPTCHA:** Zillow는 자동화된 리クエスト를 차단하기 위해 CAPTCHA를 표시할 수 있습니다.
- **허니팟:** Zillow는 봇을 탐지하고 차단하기 위해 허니팟 트랩을 사용합니다.

대규모 スクレイピング의 경우, 아래에 설명된 **Zillow Scraper API** 사용을 고려하십시오.

##  Zillow Scraper API
Bright Data [Zillow Scraper API](https://brightdata.co.kr/products/web-scraper/zillow)는 자체 인프라를 구축하거나 유지보수할 필요 없이, 대규모 Zillow 데이터를 확장 가능하고 안정적이며 번거로움 없이 추출할 수 있는 솔루션을 제공합니다.

### Key Features
- **확장 가능 & 신뢰성:** 대용량 및 실시간 데이터 수집에 최적화되어 있습니다.
- **차단 방지:** 내장 プロキシ 로ーテーション 및 CAPTCHA 해결 기능을 제공합니다.
- **법적 준수:** GDPR 및 CCPA를 완전히 준수합니다.
- **글로벌 커버리지:** 모든 지역 또는 언어에서 데이터에 접근할 수 있습니다.
- **실시간 데이터:** 지연을 최소화한 최신 데이터를 제공합니다.
- **고급 필터링:** 정밀한 필터로 데이터 추출을 사용자 지정할 수 있습니다.
- **사용량 기반 과금:** 성공한 レスポンス에 대해서만 비용을 지불합니다.
- **무료 체험:** 시작을 위한 무료 API 호출 20회를 포함합니다.
- **전담 지원:** 24/7 기술 지원을 제공합니다.
- **No-Code 옵션:** API 또는 no-code 스크레이퍼를 통해 Zillow 데이터를 スクレイピング할 수 있습니다.

### Quick Start Guide
- **가입:** [Bright Data account](https://brightdata.co.kr/)를 생성하십시오.
- **API Token 받기:** 대시보드에서 [API key](https://docs.brightdata.com/general/account/api-token)를 받으십시오.
- **エンドポイント 선택:** 아래의 사용 가능한 API エンドポイント 중에서 선택하십시오.

## 1. Zillow Property Details by URL
부동산 URL을 제공하여 부동산 상세 정보를 수집합니다.

<img width="700" alt="zillow-properties-listing-information" src="https://github.com/bright-kr/zillow-scraper/blob/main/zillow-images/zillow-properties-listing-information.png" />

### Input Parameters
| Parameter | Required | Description            |
|-----------|----------|------------------------|
| `url`       | Yes      | Zillow 부동산 URL   |


### Example Request
#### Python Code:
```python
properties = [
    {"url": "https://www.zillow.com/homedetails/73-Beverly-Park-Ln-Beverly-Hills-CA-90210/20533547_zpid/"},
    {"url": "https://www.zillow.com/homedetails/1945-N-Edgemont-St-Los-Angeles-CA-90027/20809871_zpid/"}
]
```

👉 전체 Python 스크립트: [zillow_properties.py](https://github.com/bright-kr/Zillow-Scraper/blob/main/zillow_api_scraper/zillow_properties.py)

#### cURL Command:
```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
     -H "Content-Type: application/json" \
     -d '[
           {
             "url": "https://www.zillow.com/homedetails/2506-Gordon-Cir-South-Bend-IN-46635/77050198_zpid/?t=for_sale"
           }
         ]' \
     "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_lfqkr8wm13ixtbd8f5&include_errors=true"
```

### Response Schema
```json
{
    "property_overview": {
        "address": "73 Beverly Park Ln, Beverly Hills, CA 90210",
        "price": "$89,900,000",
        "status": "FOR_SALE",
        "living_area": "28,500 sq ft",
        "lot_size": "2.68 acres",
        "bedrooms": 9,
        "bathrooms": 22,
    },
    "key_features": {
        "highlights": [
            "85-foot infinity lap pool",
            "Two kitchens (including commercial-grade)",
            "5,000 sq ft primary suite",
            "Screening room",
            "Gated community with guard",
        ],
        "views": ["City", "Ocean", "Mountain", "Canyon"],
    },
    "financial": {
        "last_sold": "2021-04-08 for $28,500,000",
        "property_tax_rate": "1.18%",
        "monthly_hoa": "$6,216",
    },
}
```

👉 이는 부분 レスポンス입니다. 전체 부동산 상세 정보는 [full JSON response](https://github.com/bright-kr/Zillow-Scraper/blob/main/zillow_api_data/zillow_properties.json)를 확인하십시오.

## 2. Zillow Properties Listing by Filters
위치 및 기타 기준을 사용하여 부동산을 검색합니다.

<img width="700" alt="zillow-properties-listing-by-input" src="https://github.com/bright-kr/zillow-scraper/blob/main/zillow-images/zillow-properties-listing-by-input.png" />

💡 **Note:** 일부 부동산은 여러 유닛을 포함할 수 있으며, 이로 인해 여러 레코드가 생성될 수 있습니다. 결과를 제한하려면 [Limit per input](https://docs.brightdata.com/scraping-automation/web-scraper-api/overview#limit-records)을 사용하십시오.

### Input Parameters
| Parameter       | Required | Description                                          |
|---------------|----------|------------------------------------------------------|
| `location`      | Yes      | 우편번호, 도시 또는 주가 될 수 있습니다.                   |
| `listingCategory` | Yes    | 옵션: Sold, House for rent, House for sale.       |
| `HomeType`      | Yes      | Zillow의 주거 유형(예: Houses, Apartments, Townhomes). |


### Example Request
#### Python Code:
```python
filters = [
    {"location": "92027", "listingCategory": "Sold", "HomeType": "Houses"},
    {"location": "New York", "listingCategory": "House for rent", "HomeType": "Condos"},
    {"location": "Colorado", "listingCategory": "", "HomeType": ""},
]
```
👉 전체 Python 스크립트: [zillow_discovered_properties.py](https://github.com/bright-kr/Zillow-Scraper/blob/main/zillow_api_scraper/zillow_discovered_properties.py)

#### cURL Command:
```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
     -H "Content-Type: application/json" \
     -d '[{"location": "New York", "listingCategory": "House for rent", "HomeType": "Houses"},
          {"location": "02118", "listingCategory": "House for sale", "HomeType": "Condos"},
          {"location": "Colorado", "listingCategory": "", "HomeType": ""}]' \
     "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_lfqkr8wm13ixtbd8f5&include_errors=true&type=discover_new&discover_by=input_filters"
```

### Response Schema
```json
{
    "address": {
        "streetAddress": "569 Hayward Pl",
        "city": "Escondido",
        "state": "CA",
        "zipcode": "92027",
    },
    "homeStatus": "SOLD",
    "bedrooms": 4,
    "bathrooms": 2,
    "livingArea": 1446,
    "livingAreaUnits": "Square Feet",
    "lotSize": 5933,
    "lotAreaUnits": "Square Feet",
    "homeType": "SINGLE_FAMILY",
    "yearBuilt": 1987,
    "lastSoldPrice": 689000,
    "dateSoldString": "2022-08-11",
    "zestimate": 818100,
    "rentZestimate": 3752,
    "schools": [
        {
            "name": "Glen View Elementary School",
            "distance": 0.6,
            "rating": 5,
            "grades": "K-5",
        },
        {
            "name": "Hidden Valley Middle School",
            "distance": 1.2,
            "rating": 5,
            "grades": "6-8",
        },
        {
            "name": "Orange Glen High School",
            "distance": 1.4,
            "rating": 5,
            "grades": "9-12",
        },
    ],
    "url": "https://www.zillow.com/homedetails/569-Hayward-Pl-Escondido-CA-92027/16696746_zpid/",
}
```

👉 이는 부분 レスポンス입니다. 전체 부동산 상세 정보는 [full JSON response](https://github.com/bright-kr/Zillow-Scraper/blob/main/zillow_api_data/zillow_discovered_properties.json)를 확인하십시오.

## 3. Zillow Properties Listing by URL
Zillow 검색 페이지 URL을 사용하여 부동산을 직접 검색합니다.

<img width="700" alt="zillow-properties-listing-by-url" src="https://github.com/bright-kr/zillow-scraper/blob/main/zillow-images/zillow-properties-listing-by-url.png" />


💡 **Note:** 일부 부동산은 여러 유닛을 포함할 수 있으며, 이로 인해 여러 레코드가 생성될 수 있습니다. 결과를 제한하려면 [Limit per input](https://docs.brightdata.com/scraping-automation/web-scraper-api/overview#limit-records)을 사용하십시오.


### Input Parameters:
| Parameter | Required | Description                          |
|-----------|----------|--------------------------------------|
| `url`       | Yes      | 완전한 검색 파라メータ를 포함한 직접 Zillow 검색 URL |

### Example Request
#### Python Code:
```python
urls = [
    {"url": "https://www.zillow.com/south-bend-in/?searchQueryState=%7B%22pagination%22%3A..."},
    {"url": "https://www.zillow.com/new-york-ny/rentals/?searchQueryState=%7B%22isMapVisible%22%3A..."},
    {"url": "https://www.zillow.com/sands-point-ny/rentals/?searchQueryState=%7B%22isMapVisible%22%3A..."},
]
```
👉 전체 Python 스크립트: [zillow_discovered_properties_by_url.py](https://github.com/bright-kr/Zillow-Scraper/blob/main/zillow_api_scraper/zillow_discovered_properties_by_url.py)

#### cURL Command:
```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
     -H "Content-Type: application/json" \
     -d '[{"url": "https://www.zillow.com/south-bend-in/?searchQueryState=%7B%22pagination%22%3A..."}]' \
     "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_lfqkr8wm13ixtbd8f5&include_errors=true&type=discover_new&discover_by=url"
```

### Response Schema:
```json
{
    "zpid": 77029580,
    "address": {
        "streetAddress": "1937 Churchill Dr",
        "city": "South Bend",
        "state": "IN",
        "zipcode": "46617",
    },
    "price": 435000,
    "bedrooms": 4,
    "bathrooms": 4,
    "livingArea": 3197,
    "lotAreaValue": 0.46,
    "lotAreaUnits": "Acres",
    "yearBuilt": 1968,
    "homeStatus": "FOR_SALE",
    "zestimate": 420400,
    "lastSoldPrice": 134000,
    "dateSold": "2013-05-20",
    "schools": [
        {"name": "McKinley Elementary School", "rating": 4},
        {"name": "Edison Intermediate Center", "rating": 2},
        {"name": "Rise Up Academy At Eggleston", "rating": 1},
    ],
    "mortgageRates": {"thirtyYearFixedRate": 6.536},
    "listingProvidedBy": {"name": "Eric M Bomkamp", "phoneNumber": "574-360-2569"},
    "url": "https://www.zillow.com/homedetails/1937-Churchill-Dr-South-Bend-IN-46617/77029580_zpid/",
}
```
👉 이는 부분 レスポンス입니다. 전체 부동산 상세 정보는 [full JSON response](https://github.com/bright-kr/Zillow-Scraper/blob/main/zillow_api_data/zillow_discovered_properties_by_url.json)를 확인하십시오.

## 4. Zillow Price History
부동산의 가격 이력을 수집합니다.

<img width="700" alt="zillow-price-history" src="https://github.com/bright-kr/zillow-scraper/blob/main/zillow-images/zillow-price-history.png" />

### Input Parameters

| Parameter | Required | Description            |
|-----------|----------|------------------------|
| `url`       | Yes      | Zillow 부동산 URL.   |

### Example Request
#### Python Code:

```python
urls = [
    {"url": "https://www.zillow.com/homedetails/8305-Blue-Heron-Way-Raleigh-NC-27615/6468808_zpid/"},
    {"url": "https://www.zillow.com/homedetails/930-3rd-St-SE-Hickory-NC-28602/71557289_zpid/"},
]
```
👉 전체 Python 스크립트: [zillow_price_history.py](https://github.com/bright-kr/Zillow-Scraper/blob/main/zillow_api_scraper/zillow_price_history.py)

#### cURL Command:
```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
     -H "Content-Type: application/json" \
     -d '[{"url": "https://www.zillow.com/homedetails/8305-Blue-Heron-Way-Raleigh-NC-27615/6468808_zpid/"},
          {"url": "https://www.zillow.com/homedetails/930-3rd-St-SE-Hickory-NC-28602/71557289_zpid/"}]' \
     "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_lxu1cz9r88uiqsosl&include_errors=true"
```

### Response Schema:
```json
{
    "url": "https://www.zillow.com/homedetails/8305-Blue-Heron-Way-Raleigh-NC-27615/6468808_zpid/",
    "zpid": "6468808",
    "date": "2020-11-13T00:00:00.000Z",
    "event": "Sold",
    "price": 440000,
    "price_per_squarefoot": 127,
    "source": "Doorify MLS",
    "timestamp": "2025-02-09T16:56:42.074Z",
}
```
👉 이는 부분 レスポンス입니다. 전체 부동산 상세 정보는 [full JSON response](https://github.com/bright-kr/Zillow-Scraper/blob/main/zillow_api_data/zillow_price_history.json)를 확인하십시오.

## No-Code Scraper Option
Bright Data **No-Code Scraper**는 프로그래밍 없이 Zillow 데이터를 수집할 수 있는 사용자 친화적인 방법을 제공합니다.
- 몇 분 만에 스크레이퍼를 구성할 수 있습니다.
- 전체 데이터 수집 프로세스를 자동화할 수 있습니다.
- 여러 형식으로 결과를 직접 다운로드할 수 있습니다.

자세한 안내는 [Getting Started guide](https://github.com/bright-kr/Zillow-Scraper/blob/main/no-code-scraper.md)를 방문하십시오.

## Additional Options
다음 파라メータ로 데이터 수집을 세밀하게 조정하십시오:

| **Parameter**       | **Type**   | **Description**                                            | **Example**                  |
|---------------------|------------|------------------------------------------------------------|------------------------------|
| `limit`             | `integer`  | 입력당 최대 결과 수                                   | `limit=10`                   |
| `include_errors`    | `boolean`  | 문제 해결을 위한 오류 보고서 받기                     | `include_errors=true`        |
| `notify`            | `url`      | 완료 시 알림을 받기 위한 웹훅 알림 URL  | `notify=https://notify-me.com/` |
| `format`            | `enum`     | 출력 형식(예: JSON, NDJSON, JSONL, CSV)         | `format=json`                |

💡 **Pro Tip:** 데이터를 [external storage](https://docs.brightdata.com/scraping-automation/web-data-apis/web-scraper-api/overview#via-deliver-to-external-storage) 또는 [webhook](https://docs.brightdata.com/scraping-automation/web-data-apis/web-scraper-api/overview#via-webhook)으로 전달할 수 있습니다.

## Support & Resources
- **API Documentation:** [Bright Data Docs](https://docs.brightdata.com/scraping-automation/web-scraper-api/trigger-a-collection)
- **스크레이핑 모범 사례:** [Avoid Getting Blocked](https://brightdata.co.kr/blog/web-data/web-scraping-without-getting-blocked)
- **기술 지원:** [Contact Us](mailto:support@brightdata.com)