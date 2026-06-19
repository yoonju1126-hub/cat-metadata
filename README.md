# 고양이 통합 메타데이터 스키마 최종 프로젝트 웹사이트 (Unified Cat Metadata Schema)

## Section A. 서론 (Opening Narrative)

### 1. 도메인 영역 내 메타데이터의 역사
고양이라는 도메인은 인류의 역사 속에서 단순한 반려동물을 넘어 생물학적 연구 대상, 박물관의 고고학적 유물, 그리고 현대의 가상 캐릭터 및 디지털 IP에 이르기까지 매우 다채롭고 복잡한 스펙트럼을 지니고 있습니다. 그러나 기존의 표준 정보 기술들은 이러한 다면성을 개별적으로만 다룰 뿐, 하나의 유기적인 스키마로 통합하지 못했습니다. 
예를 들어 생물다양성 표준인 Darwin Core(DwC)는 고양이의 생물학적 분류를 기록할 수 있지만 박물관 유물로서의 역사적 가치를 담지 못하며, VRA Core나 CDWALite 같은 문화재 표준은 살아있는 생명체의 생애 주기나 의료 상태를 추적하는 데 한계가 있었습니다. 이에 현실(Reality), 역사(History), 가상 및 지식재산권(IP)을 모두 아우를 수 있는 고양이 전용 통합 메타데이터 스키마를 고안하게 되었습니다.

### 2. 예상 사용자 (Intended Users)
* **동물 보호소 및 유관 기관:** 유기묘 구조, 입양 이력 관리, TNR(Trap-Neuter-Return) 상태 및 예방접종 등 의료 상태 관리자.
* **아카이브 및 박물관 큐레이터:** 자연사 박물관의 고양이 골격 표본, 고고학 박물관의 고양이 미라 유물 등 역사적 유산 관리자.
* **미디어 및 디지털 콘텐츠 에이전시:** 가상 캐릭터(Hello Kitty 등) 라이선싱 관리자, 유명 인플루언서 고양이의 디지털 권리 및 소셜 미디어 핸들 관리자.

### 3. 스키마 개발 프로세스 노트 (Development Notes)
본 스키마는 초안 1부터 4까지의 엄격한 고도화 단계를 거쳐 완성되었습니다.
* **Draft 1 ~ 2 (개념 정립 및 벤치마킹):** 고양이의 특수성을 반영하기 위해 생물학(DwC), 서지/권리(DC), 이력 보존(PREMIS), 구조적 프레임워크(VRA Core) 등 다양한 표준 스키마를 분석 및 채택했습니다. 또한, 집고양이부터 이집트 미라, 헬로키티, 인플루언서 고양이까지 총 10개의 다채로운 검사 코퍼스(Exemplar Objects)를 설정하여 필수 요소를 도출했습니다.
* **Draft 3 (어휘 명세 및 데이터 사전):** 핵심 12개 요소를 확정하고, 중성화 방사(TNR), 구조(Rescue) 등을 포함하는 이력 통제어휘(Appendix A)와 가상/야생 등을 구분하는 사육 상태 통제어휘(Appendix B)를 구축했습니다.
* **Draft 4 & Final (XSD 구현 및 기술적 예외 처리):** XML Schema(XSD)를 설계하는 과정에서, 로컬 VS Code IDE의 네트워크 프록시 및 방화벽 오류로 인해 원격 XML 스키마를 실시간으로 가져오지 못하는 기술적 제약이 발생했습니다. 다수의 로컬 지원 파일이 파편화되거나 스키마가 비대해지는 것을 방지하기 위해, 외부 표준 요소를 무리하게 원격 참조하는 대신 표준 네임스페이스 의미론을 준수하되 로컬 스키마 프레임워크 내에 유연하게 내장·바인딩하는 방식으로 설계를 보완했습니다.

### 4. 주요 이론적 고려 사항 (Theoretical Considerations)
본 스키마는 예술품 기술 표준인 **VRA Core의 '래퍼 구조(Wrapper Structure)'** 개념을 이론적 기반으로 삼고 있습니다. VRA Core가 개념적 'Work(작품)'와 물리적 'Image(도상)'를 깔끔하게 분리하듯, 본 스키마 역시 `catRecord`라는 최상위 루트 래퍼를 통해 고양이 객체의 영속적인 핵심 데이터(Core Data)를 선언하고, 그 하위에 의료 상태나 연대기적 이력 사건(Provenance Events)과 같이 확장 및 생략이 가능한 가변적 모듈식 인스턴스를 계층적으로 배치하여 정보의 복잡성을 통제하도록 설계했습니다.

---

## Section B. 관련 메타데이터 표준 (Relevant Metadata Standards)

상호운용성(Interoperability)을 극대화하기 위해 본 스키마에 매핑 및 구현된 기존 국제 표준 표준은 다음과 같습니다.

* **Dublin Core (dc):** 객체의 가장 기본적인 발견 가능성을 확보하기 위해 사용되었습니다. 고양이 객체의 명칭인 `title`과 복잡한 저작권 및 소유권 관계를 명시하기 위한 `rights` 요소의 표준 기반이 됩니다.
* **Darwin Core (dwc):** 고양이가 생물학적 유기체이거나 자연사 표본일 때 학술적 교환이 가능하도록 과학적 학명 표준인 `scientificName`을 엄격하게 수용하기 위해 채택했습니다.
* **PREMIS (premis):** 고양이의 생애 주기(구조, 입양, TNR) 및 유물의 역사적 사건(미라화 등)을 기계가 읽을 수 있고 유효성 검증이 가능한 연대기적 시퀀스로 추적하기 위해 Event 기반 구조를 차용했습니다.
* **VRA Core (vra):** 데이터가 늘어나도 파편화되지 않고 유기적으로 묶일 수 있도록 전체 스키마를 관장하는 계층형 '래퍼(Wrapper)' 구조의 골격을 빌려왔습니다.

---

## Section C. 어휘 명세서 (Vocabulary Specification)

### 1. 요소 개요 테이블 (Element Overview Table)

| 요소명 (Element Name) | 정의 및 설명 (Definition) | 수량 제약 (Occurrence) | 데이터 타입 (Data Type) | 매핑 표준 (Alignment) |
| :--- | :--- | :--- | :--- | :--- |
| **catRecord** | 고양이 통합 메타데이터 레코드의 최상위 루트 래퍼 | 필수 (1) | Complex Type | VRA Core (Structure) |
| **title** | 고양이 객체에 부여된 공식 이름 또는 타이틀 | 필수 (1) | `xs:string` | dc:title |
| **identifier** | 로컬 개체 식별을 위한 고유 제어 번호 또는 문자열 | 필수 (1) | `xs:string` | Local Identifier |
| **scientificName** | 생물학적 분류법에 따른 고양이의 정식 학명 | 필수 (1) | `xs:string` | dwc:scientificName |
| **breed** | 로컬 품종명 또는 외형적 변종 명칭 (중복 가능) | 선택 (0..*) | `xs:string` | Local (ex:breed) |
| **domesticationStatus**| 현실, 역사, 가상을 아우르는 사육 및 생태 상태 | 필수 (1) | Controlled Vocab | Local (ex:domestication) |
| **physicalState** | 생명체, 미라 유물, 디지털 자산 등 물리적 상태 구분 | 선택 (0..1) | `xs:string` | Local Physical State |
| **agent** | 객체와 연관된 소유자, 기관, 관리자, 창작자 등 | 선택 (0..*) | `xs:string` | Local Agent |
| **currentLocation** | 객체가 현재 위치한 물리적 장소 또는 소속 기관 | 선택 (0..1) | `xs:string` | Local Location |
| **medicalStatus** | 진행 중인 건강 상태 혹은 유물의 보존 환경 요약 | 선택 (0..1) | `xs:string` | Local Medical Status |
| **socialPresence** | SNS 핸들, 웹 링크, 전시 카탈로그 ID 정보 | 선택 (0..1) | `xs:string` | Local Presence |
| **rights** | 레코드 및 객체에 할당된 저작권 및 지식재산권 선언 | 필수 (1) | `xs:string` | dc:rights |
| **provenanceHistory** | 행정적/생애적 이력 사건들을 담는 통제 래퍼 | 선택 (0..1) | Complex Type | PREMIS (Wrapper) |

---

### 2. 전체 데이터 사전 (Data Dictionary)

#### 1) 단일 요소 및 통제 어휘 명세
* **domesticationStatusType (통제 어휘)**
  * **정의:** 고양이 객체의 실존 성격 및 생태적 환경을 제한하는 4가지 범위의 통제 어휘입니다.
  * **허용 값 (Enumeration):**
    * `Domesticated`: 인간과 밀접하게 생활하는 반려 개체.
    * `Feral`: 가축화되었으나 야생에서 생활하는 개체(길고양이 등).
    * `Wild`: 자연 상태의 야생 고양이 종.
    * `Fictional`: 실제 생명체가 아닌 가공의 존재.
* **breed (품종)**
  * **설계 의도:** Darwin Core 표준의 `dwc:taxonRank`는 생물학적으로 '품종(Breed)' 단위를 표현하는 데 제한이 따릅니다. 따라서 고양이 도메인의 핵심 속성을 살리기 위해 믹스견/품종 혼합 처리가 가능하도록 다중값(`maxOccurs="unbounded"`) 표기가 가능한 로컬 요소로 대체 신설했습니다.

#### 2) 이력 관리 복합 요소 구조 (provenanceHistory)
* **provenanceEvent (반복 가능 이력 사건 단위):** 고양이 개체에 일어난 연대기적 사건을 기계 유효성 검증이 가능한 중첩 시퀀스로 캡슐화합니다.
  * **eventType:** 수행된 행동의 유형을 기술합니다 (`Rescue`, `TNR`, `Adoption`, `Certification`, `Mummification` 등).
  * **eventDateTime:** 사건이 발생한 날짜 및 시간적 지표를 표기합니다. (예: `2024-05-12` 또는 역사적 모호성을 위한 `c. 332 BC` 등 허용)
  * **eventDetail:** 사건과 관련된 상세 정보나 장소, 추가 노트를 기록합니다 (`minOccurs="0"`).

---

## Section D. XSD 파일 (cat_schema.xsd)

본 메타데이터 스키마의 무결성을 검증하기 위한 정식 XML Schema(XSD) 주소입니다. 샘플 XML 레코드들이 참조하고 유효성 검사(Validation)를 수행할 수 있도록 아래와 같이 직통 URL(Raw URL)을 공유합니다.

* **XSD 파일 직통 URL:** https://github.com/yoonju1126-hub/cat-metadata/raw/refs/heads/main/cat_schema.xsd

---

## Section E. 샘플 XML 레코드 (Sample XML Records)

제작된 `cat_schema.xsd` 파일 규칙을 100% 만족하며 완벽히 유효성 검증(Validation)을 통과하는 실무 데이터 인스턴스 2종입니다.

### 1. 반려묘 인스턴스: 집고양이 '나비' (`record_domestic.xml`)
* **설명:** 현실의 생명체이자 반려묘로서의 데이터를 증명하는 레코드입니다. 예외 처리된 로컬 품종(`breed`) 요소와 구조 및 입양이라는 연속적 생애 주기(PREMIS 기반 이력)가 원활하게 기록됨을 입증합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<catRecord xmlns="http://example.org/cat/schema/"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://example.org/cat/schema/ cat_schema.xsd">

    <title>Nabi (집고양이 나비)</title>
    <identifier>PET-2026-042</identifier>
    <title>Nabi (집고양이 나비)</title>
    <identifier>PET-2026-042</identifier>
    <scientificName>Felis catus</scientificName>
    <breed>Mixed Breed</breed>
    <domesticationStatus>Domesticated</domesticationStatus>
    <physicalState>Living Organism</physicalState>
    <agent>Oh Yoonju (Owner)</agent>
    <currentLocation>Seoul, South Korea</currentLocation>
    <medicalStatus>Healthy, Indoor status</medicalStatus>
    <rights>Private Personal Data. All rights reserved by the owner.</rights>
    
    <provenanceHistory>
        <provenanceEvent>
            <eventType>Rescue</eventType>
            <eventDateTime>2024-05-12</eventDateTime>
            <eventDetail>Rescued near Mapo-gu street alleyways.</eventDetail>
        </provenanceEvent>
        <provenanceEvent>
            <eventType>Adoption</eventType>
            <eventDateTime>2024-06-01</eventDateTime>
            <eventDetail>Officially adopted into the current household.</eventDetail>
        </provenanceEvent>
    </provenanceHistory>

</catRecord>

2. 고고학 아카이브 인스턴스: '고대 이집트 고양이 미라' (record_mummy.xml)
설명: 역사적 유물이자 인공물(Artifact)로서의 데이터를 증명하는 레코드입니다. 보존 환경(medicalStatus 요소의 유연한 전용), 전시 정보(socialPresence), 기원전 기원 및 미라화 과정에 대한 역사적 이력이 깨짐 없이 완벽히 유효성 검증을 통과합니다.

<?xml version="1.0" encoding="UTF-8"?>
<catRecord xmlns="http://example.org/cat/schema/"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://example.org/cat/schema/ cat_schema.xsd">

    <title>Ancient Egyptian Cat Mummy</title>
    <identifier>ARC-2026-M09</identifier>
    <scientificName>Felis catus</scientificName>
    <breed>Domestic Short Hair</breed>
    <domesticationStatus>Domesticated</domesticationStatus>
    <physicalState>Organic Artifact / Desiccated Remains</physicalState>
    <agent>Free Museum of Antiquities (Current Custodian)</agent>
    <currentLocation>Gallery 3, Case B - Egyptian Antiquities Wing</currentLocation>
    <medicalStatus>Stable, preserved in low-humidity vitrine</medicalStatus>
    <socialPresence>Exhibition Catalog Entry ID: #EGY-CAT-332</socialPresence>
    <rights>Copyright © 2026 Free Museum of Antiquities. Licensed under CC BY-NC 4.0.</rights>
    
    <provenanceHistory>
        <provenanceEvent>
            <eventType>Mummification</eventType>
            <eventDateTime>c. 332 BC</eventDateTime>
            <eventDetail>Location: Abydos, Egypt. Ritual votive offering preparation.</eventDetail>
        </provenanceEvent>
    </provenanceHistory>

</catRecord>
