---
title: Dighist Mappings
layout: default
nav_order: 4
---

# Other mappings of Digital History

I enjoyed making the 'transformations' diagram on the [schedule](schedule) page so much, I may have gotten carried away trying alternative configurations of the mermaid diagram. Each movement from one box (or branch) of a diagram constitutes a moment where theory and method collide.

## Dighist as a series of 'states'

```mermaid
stateDiagram-v2
    [*] --> PhysicalState: Discovery & Acquisition
    
    state PhysicalState {
        [*] --> RawMaterial
        RawMaterial --> CuratedCollection
        CuratedCollection --> ArchivalStorage
    }
    
    PhysicalState --> DigitalState: Digitization (Scanning, 3D, ASR)
    
    state DigitalState {
        [*] --> RawDigitalProxy
        RawDigitalProxy --> WebAccessibleMedia
    }
    
    DigitalState --> DataState: Data Extraction (OCR, TEI, Transcription)
    
    state DataState {
        [*] --> MachineReadableText
        MachineReadableText --> StructuredData (JSON)
        StructuredData (JSON) --> LinkedOpenData
    }
    
    DataState --> AnalyticalState: Computational Analysis
    
    state AnalyticalState {
        [*] --> ExtractedEntities
        ExtractedEntities --> Visualizations (Maps, Networks)
    }
    
    AnalyticalState --> DigitalState: Publish Findings
    
    DataState --> PreservationState: Ingestion
    WebAccessibleMedia --> PreservationState: Web Archiving
    
    state PreservationState {
        [*] --> InstitutionalRepository
        InstitutionalRepository --> CitableDataset (DOI)
    }
    
    CitableDataset (DOI) --> [*]
```

## Dighist with more kinds of evidence

```mermaid
flowchart TD
    %% --- Define Styling Classes ---
    classDef source fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#000
    classDef physical fill:#fff3e0,stroke:#e65100,stroke-width:2px,color:#000
    classDef digital fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#000
    classDef data fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#000
    classDef analysis fill:#fff8e1,stroke:#f57f17,stroke-width:2px,color:#000
    classDef preservation fill:#eceff1,stroke:#546e7a,stroke-width:2px,color:#000

    %% --- 1. Original Sources ---
    subgraph Original_Materials [Original Source Materials]
        D([Diaries]):::source
        PH([Photos]):::source
        F([Films]):::source
        V([Videos]):::source
        AU([Audio / Cassettes]):::source
        PO([Physical Objects]):::source
        SITE([Architecture & Sites]):::source
        BD([Born Digital Materials]):::source
        OM([Other Materials]):::source
    end

    %% --- 2. Physical & Institutional Curation ---
    subgraph Physical_Curation [Physical Curation & Publication]
        HJ([Handwritten Journals]):::physical
        L([Letters]):::physical
        PUB([Publications]):::physical
        A([Archives]):::physical
        MC([Museum Collections]):::physical
        PC([Sold / Private Collections]):::physical
    end

    %% --- 3. Digitization & Web ---
    subgraph Web_Access [Digitization & Web Publishing]
        DW([Digitized for the Web]):::digital
        DF([Films Digitized]):::digital
        DA([Digitized Audio]):::digital
        P3D([Photogrammetry / Lidar]):::digital
        M3D([3D Models]):::digital
        YTV([YouTube or Vimeo]):::digital
        CE([Clips Embedded in Websites]):::digital
        PW([Published to the Web]):::digital
    end

    %% --- 4. Data Extraction & Enhancement ---
    subgraph Data_Processing [Data Extraction & Enhancement]
        PIR([Photos, Images, Digital Renderings]):::data
        OCR([Transcribed using OCR]):::data
        CROWD([Crowdsourced Transcription]):::data
        ASR([Automated Speech Recognition]):::data
        TXT([Text]):::data
        TEI([TEI / XML Markup]):::data
        J([Represented in JSON]):::data
        CLEAN([Data Wrangling / OpenRefine]):::data
        LOD([Linked Open Data]):::data
    end

    %% --- 5. Analytical Transformations ---
    subgraph Analysis [Analytical Transformations]
        NER([Named Entity Recognition]):::analysis
        NET([Network Graphs]):::analysis
        GEO([Geoparsing / Geocoding]):::analysis
        MAPS([Interactive GIS Maps]):::analysis
        TM([Topic Modeling / Text Analysis]):::analysis
    end

    %% --- 6. Digital Preservation ---
    subgraph Preservation [Preservation & End-of-Life]
        WARC([Web Archiving / WARC files]):::preservation
        REPO([Institutional Repositories]):::preservation
        DOI([Citable Datasets & DOIs]):::preservation
    end

    %% --------------------------------
    %% Flow Relationships / Edges
    %% --------------------------------

    %% Diaries paths
    D --> HJ
    HJ --> PUB
    D --> L
    L --> A

    %% Photos paths
    PH --> PUB
    PH --> A

    %% Web Digitization paths
    PUB --> DW
    A --> DW

    %% Film & Video paths
    F --> DF
    DF --> YTV
    YTV --> CE
    V --> A

    %% Audio Pathways (NEW)
    AU --> DA
    DA --> ASR
    ASR --> TXT
    DA --> PW

    %% Physical Object & 3D Pathways (NEW)
    PO --> MC
    PO --> A
    PO --> PC
    PO --> P3D
    SITE --> P3D
    P3D --> M3D
    M3D --> PW

    %% Publishing to Web
    MC --> PW
    A --> PW
    PC --> PW
    CE --> PW
    DW --> PW

    %% Bridging Web Assets into Data Processing
    DW --> PIR
    PW --> PIR

    %% OCR, Crowdsourcing, and Text Pipeline (EXPANDED)
    PIR --> OCR
    PIR --> CROWD
    OCR --> TXT
    CROWD --> TXT
    TXT --> TEI
    
    %% Compilation into JSON and Cleaning (EXPANDED)
    TEI --> J
    TXT --> J
    OM --> J
    BD --> J
    J --> CLEAN
    CLEAN --> LOD

    %% Analytical Pipelines (NEW)
    TXT --> NER
    NER --> NET
    NER --> GEO
    GEO --> MAPS
    TXT --> TM

    %% Sending Analysis back to the Web (NEW)
    MAPS --> PW
    NET --> PW

    %% Preservation & Archiving Pipelines (NEW)
    PW --> WARC
    LOD --> REPO
    CLEAN --> REPO
    TM --> REPO
    REPO --> DOI

    %% The Lifecycle Loop: Preserved Data becomes a new Source (NEW)
    DOI -.->|Re-enters Research Cycle as a new Source| BD
```

## Dighist as Mindmap

```mermaid
mindmap
  root((Digital History<br/>Lifecycle))
  
    Original Sources
      Textual
        [Diaries]
        [Letters]
        [Journals]
      Audio Visual
        [Photos]
        [Films & Videos]
        [Audio Cassettes]
      Physical & Spatial
        [Physical Objects]
        [Architecture & Sites]
      Digital
        [Born Digital Materials]

    Physical Curation
      Institutions
        {{Archives}}
        {{Museum Collections}}
      Private Domain
        {{Sold / Private Collections}}
      Outputs
        {{Physical Publications}}

    Digitization & Web
      Imaging & 3D
        (2D Digitized Images)
        (Photogrammetry & Lidar)
        (3D Models)
      A/V Platforms
        (Digitized Audio)
        (Digitized Video)
        (YouTube / Vimeo)
      Publishing
        (Websites & Online Exhibits)

    Data Extraction & Enhancement
      Transcription
        [OCR]
        [Crowdsourcing]
        [Automated Speech Recognition]
      Structuring Data
        [Plain Text]
        [TEI / XML Markup]
        [JSON]
      Refinement
        [Data Wrangling / OpenRefine]
        [Linked Open Data]

    Analytical Transformations
      Text Analysis
        (Named Entity Recognition)
        (Topic Modeling)
      Spatial Analysis
        (Geoparsing & Geocoding)
        (Interactive GIS Maps)
      Relational
        (Network Graphs)

    Digital Preservation
      Web 
        {{Web Archiving / WARC Files}}
      Data
        {{Institutional Repositories}}
        {{Citable Datasets & DOIs}}
          [Re-enters Cycle as Born-Digital Source]
```