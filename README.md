# Monocular Vision-Based Predictive Digital Twin for Road Infrastructure Maintenance Optimisation

![Project](https://img.shields.io/badge/Project-Capstone-blue)
![Domain](https://img.shields.io/badge/Domain-AI%20%2F%20ML-orange)
![Institution](https://img.shields.io/badge/Institution-PES%20University-navy)
![Status](https://img.shields.io/badge/Status-In%20Development-yellow)

## 1. Project Overview

**Project ID:** PW26_VK_02\
**Course:** UE24AM320A -- Capstone Project Phase-I\
**Programme:** B.Tech CSE (Artificial Intelligence & Machine Learning)\
**Academic Year:** 2024--2028\
**Semester:** V\
**Project Guide:** Dr. Vidhya K

### Abstract

Road infrastructure maintenance is predominantly reactive, with repairs
often initiated only after visible deterioration or public complaints.
Existing road-monitoring solutions frequently depend on expensive
infrastructure such as LiDAR, drones, and specialised sensors, making
them difficult to deploy at scale, particularly for local municipal
authorities.

This project proposes a **Monocular Vision-Based Predictive Digital
Twin** that uses ordinary dashcam or smartphone video to monitor road
conditions, estimate pothole severity, track deterioration over time,
and prioritise maintenance activities.

The system aims to integrate computer vision, monocular depth
estimation, geospatial mapping, weather and traffic context,
uncertainty-aware forecasting, and budget-conscious repair
prioritisation into a unified digital twin.

The ultimate goal is to enable data-driven, proactive and cost-effective
road infrastructure maintenance using affordable sensing technologies.

## 2. Problem Statement

Current road maintenance practices face several limitations:

-   Road repairs are primarily reactive rather than predictive.
-   Existing digital twin solutions often require expensive sensing
    infrastructure.
-   Conventional phone and dashcam-based systems primarily focus on
    damage detection rather than long-term deterioration tracking.
-   Monocular depth estimates may contain significant measurement
    errors.
-   Maintenance prioritisation often lacks uncertainty-aware forecasting
    and budget-conscious decision-making.

**Our central research question:**

Can ordinary geotagged dashcam video support reliable road-condition
monitoring, deterioration forecasting and repair prioritisation while
explicitly accounting for measurement uncertainty?

## 3. Project Objectives

The project focuses on the following objectives:

1.  Detect and segment road distress using geotagged dashcam footage.
2.  Estimate pothole depth using monocular vision and provide calibrated
    uncertainty intervals.
3.  Build a longitudinal digital twin by tracking fixed 20-metre road
    cells across repeated surveys.
4.  Incorporate historical weather conditions and traffic-related
    deterioration indicators.
5.  Forecast the progression of early road distress using
    uncertainty-aware models.
6.  Rank road segments for maintenance based on risk, severity and
    uncertainty.
7.  Develop a dashboard for visualising road conditions, deterioration
    history, forecasts and repair priorities.

## 4. Proposed System Architecture

The proposed system follows an end-to-end pipeline:

``` text
Dashcam / Smartphone Video
          +
     GPS / GPX Data
          |
          v
   Road Damage Detection
          |
          v
  Damage Segmentation
          |
          v
 Monocular Depth Estimation
   + Uncertainty Intervals
          |
          v
   GPS Mapping to Fixed
       20m Road Cells
          |
          v
   Contextual Information
  - Historical Weather
  - Traffic Exposure Proxy
  - Road Characteristics
          |
          v
     Digital Twin
  - Cell Condition
  - Historical Records
  - Repair Events
          |
          v
 Deterioration Forecasting
   + Prediction Uncertainty
          |
          v
   Repair Prioritisation
          |
          v
     Web Dashboard
```

An important design principle is that depth uncertainty must propagate
downstream into severity estimation, deterioration forecasting and
repair prioritisation rather than being discarded after depth
estimation.

## 5. Methodology and Technology Stack

  Component                Proposed Method / Technology
  ------------------------ ----------------------------------------------
  Road damage detection    YOLO-based detection and segmentation
  Dataset                  RDD2022 and project-collected road images
  Segmentation             Fine-tuned YOLO segmentation
  Monocular depth          Depth Anything V2 Metric
  Depth calibration        Camera calibration and road-plane fitting
  Uncertainty estimation   Cross-conformal prediction / Jackknife+
  Object tracking          ByteTrack
  GPS mapping              GPX processing and map matching
  Weather data             Open-Meteo / ERA5
  Road attributes          OpenStreetMap
  Traffic estimation       YOLO and ByteTrack-based heavy-vehicle index
  Forecasting              Bayesian / hazard models
  Repair optimisation      Uncertainty-aware prioritisation
  Visualisation            Interactive dashboard

*These are the proposed technology choices from the project design and
are subject to implementation and evaluation.*

## 6. Research Contributions and Novelty

The project focuses on three primary candidate contributions:

### 6.1 Calibrated Monocular Severity Estimation

Estimate pothole depth using a single camera without requiring LiDAR or
stereo cameras.

The estimated depth will be accompanied by an uncertainty interval,
evaluated against physically measured pothole depths.

### 6.2 Longitudinal Road Digital Twin

Create a digital representation of real road segments using repeated
surveys and fixed 20-metre cells.

The digital twin will maintain:

-   Road-cell identification.
-   Historical condition records.
-   Weather and traffic-related contextual information.
-   Pothole and distress progression.
-   Repair-event history.

### 6.3 Uncertainty-Aware Repair Prioritisation

Develop a repair prioritisation mechanism that accounts for:

-   Estimated road severity.
-   Probability of deterioration.
-   Measurement uncertainty.
-   Available maintenance budgets.

The objective is to improve maintenance decisions compared with
conventional worst-first and deterministic budget-selection approaches.

## 7. Dataset and Field Study Plan

The initial field study is designed around:

  Parameter                      Planned Scope
  ------------------------------ ---------------------------------------
  Road segments                  4
  Road ownership                 One road per team member
  Cell length                    Fixed 20 metres
  Survey frequency               Weekly
  Survey rounds                  6--12
  Physically measured potholes   Approximately 15--20
  Weather context                7, 30 and 90-day historical lookbacks

### Data Sources

-   **RDD2022:** Public road damage detection dataset.
-   **Project-collected footage:** Geotagged dashcam recordings.
-   **Open-Meteo / ERA5:** Historical weather information.
-   **OpenStreetMap:** Road characteristics and infrastructure
    attributes.
-   **Physical measurements:** Ground-truth pothole depth measurements.

Real and simulated data will be clearly distinguished during
experimentation.

## 8. Functional Requirements

  -----------------------------------------------------------------------
  ID                                  Requirement
  ----------------------------------- -----------------------------------
  FR1                                 Import video with GPS and timestamp
                                      information.

  FR2                                 Detect and segment road distress
                                      and map it to fixed cells.

  FR3                                 Estimate pothole depth with an
                                      uncertainty interval.

  FR4                                 Maintain road-cell history and
                                      repair records.

  FR5                                 Incorporate weather, road
                                      attributes and traffic proxies.

  FR6                                 Estimate short-horizon
                                      deterioration probabilities.

  FR7                                 Rank road cells for repair using
                                      risk, severity and uncertainty.
  -----------------------------------------------------------------------

### Non-Functional Requirements

-   Reproducibility through fixed protocols and versioned datasets.
-   Traceability between predictions, video frames, GPS coordinates and
    labels.
-   Robustness against poor footage and GPS misalignment.
-   Privacy protection through face and number-plate blurring.
-   Dashboard usability with understandable risk and confidence
    information.

## 9. Evaluation Strategy

The project will evaluate the individual components and the complete
pipeline.

  -----------------------------------------------------------------------
  Component                           Evaluation
  ----------------------------------- -----------------------------------
  Detection and segmentation          Detection and segmentation
                                      performance

  Depth estimation                    Depth error in centimetres

  Uncertainty estimation              Prediction interval coverage and
                                      width

  Cell mapping                        Consistency of road-cell
                                      assignments

  Forecasting                         Forecast error and progression
                                      probability calibration

  Repair prioritisation               Road condition improvement under
                                      equal budgets
  -----------------------------------------------------------------------

### Planned Baselines and Ablations

-   Uncalibrated Depth Anything V2.
-   Persistence and straight-line deterioration forecasting.
-   Visual-only versus weather and traffic-enhanced forecasting.
-   Point-depth estimates versus uncertainty-aware estimates.
-   Worst-first versus budget-aware repair selection.

Evaluation will include chronological holdout and leave-one-segment-out
testing.

## 10. Project Scope and Limitations

### In Scope

-   Four monitored road segments.
-   Monocular camera-based road monitoring.
-   Pothole depth estimation and uncertainty calibration.
-   Fixed-cell longitudinal tracking.
-   Weather and traffic-context integration.
-   Deterioration forecasting.
-   Repair prioritisation and dashboard development.

### Planned Extensions

-   Road curvature and driver-behaviour analysis.
-   Prediction before visible damage occurs.
-   Expansion to larger road networks.
-   More extensive vehicle-dynamics and traffic information.

### Known Limitations

-   Limited longitudinal observations.
-   GPS positioning errors.
-   Limited ground-truth pothole measurements.
-   Traffic measurements are relative proxies, not actual axle loads.
-   Weather information may have coarse spatial resolution.
-   Monocular depth estimation has inherent geometric limitations.
-   Initial findings are scoped to four roads within one climate.

## 11. Team Members and Responsibilities

**Project Guide:** Dr. Vidhya K

 ## 11. Team Members and Responsibilities

**Project Guide:** Dr. Vidhya K

| Team Member | SRN | Assigned Road | Proposed Responsibility |
|---|---|---|---|
| Krishna G Pai | PES1UG24AM372 | Road A | Detection and segmentation backbone; digital twin database |
| Aryaman DK | PES1UG24AM344 | Road B | Monocular depth estimation, camera calibration and uncertainty |
| Kshitij Satish Shetty | PES1UG24AM143 | Road C | Field data collection, weather and traffic features, and deterioration forecasting |
| Mallikarjuna Rao R.V. | PES1UG24AM155 | Road D | Physical pothole measurements, repair prioritisation and dashboard |

**Shared Responsibilities:** Repeat road surveys, label review, evaluation, research documentation and final report preparation.

*The road assignments and individual responsibilities reflect the proposed allocation in Review 2 and should be updated if the team or project guide revises them.*
## 12. Project Timeline

The project is planned across Capstone Phase-I and Phase-II over 12
months.

  -----------------------------------------------------------------------
  Stage                               Major Activities
  ----------------------------------- -----------------------------------
  Initial phase                       Literature survey, research gap
                                      identification and novelty
                                      validation

  Data collection                     Protocol finalisation, camera
                                      calibration and pilot surveys

  Field study                         Repeated weekly surveys and
                                      ground-truth measurements

  Model development                   Detection, segmentation and
                                      monocular depth estimation

  Forecasting                         Deterioration prediction and
                                      uncertainty modelling

  Optimisation                        Repair prioritisation and dashboard
                                      integration

  Final phase                         Evaluation, ablation studies,
                                      documentation and demonstration
  -----------------------------------------------------------------------

Field surveys are intended to begin early because longitudinal
observations cannot be reconstructed retrospectively.

## 13. Repository Structure

The repository will progressively organise the implementation and
documentation.

``` text
Capstone/
│
├── docs/
│   ├── Review1_PW26_VK_02.pptx
│   ├── Review2_PW26_VK_02.pptx
│   └── Literature_Survey_Report_PES1UG24AM155.docx
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── annotations/
│
├── models/
│   ├── detection/
│   ├── segmentation/
│   ├── depth/
│   └── forecasting/
│
├── src/
│   ├── perception/
│   ├── depth_estimation/
│   ├── geospatial/
│   ├── digital_twin/
│   ├── forecasting/
│   └── optimisation/
│
├── dashboard/
│
├── experiments/
│
├── tests/
│
├── requirements.txt
├── .gitignore
└── README.md
```

*The structure above is the proposed organisation; directories will be
added as implementation progresses.*

## 14. Expected Outcome

The expected outcome is an integrated prototype capable of:

-   Processing ordinary geotagged road videos.
-   Identifying and measuring visible road distress.
-   Estimating pothole depth with calibrated uncertainty.
-   Tracking road conditions over repeated surveys.
-   Forecasting deterioration using environmental and traffic context.
-   Prioritising maintenance activities under budget constraints.
-   Presenting road conditions and maintenance recommendations through
    an interactive dashboard.

The project aims to demonstrate how affordable monocular vision systems
can support more proactive, transparent and data-driven road
infrastructure maintenance.

## 15. References and Further Reading

The research is based on the literature survey consolidated during
Review 1 and extended during Review 2.

Key references and technologies include:

1.  Yang et al., *Depth Anything V2*, NeurIPS, 2024.
2.  Arya et al., *RDD2022: A Multi-National Image Dataset for Automatic
    Road Damage Detection*, Geoscience Data Journal, 2024.
3.  Zhang et al., *ByteTrack: Multi-Object Tracking by Associating Every
    Detection Box*, ECCV, 2022.
4.  Hersbach et al., *The ERA5 Global Reanalysis*, Quarterly Journal of
    the Royal Meteorological Society, 2020.
5.  Barber et al., *Predictive Inference with the Jackknife+*, Annals of
    Statistics, 2021.
6.  Wang et al., *Video-Based Pothole Detection and Area Estimation with
    Depth Map and Kalman Smoothing*, arXiv:2505.21049, 2025.
7.  Shakya et al., *Pavement Deterioration on Nepal National Highways*,
    Infrastructures, 2025.
8.  Talaghat et al., *Road Pavement Digital Twin: A Blueprint with a
    Case Study*, Journal of Computing in Civil Engineering, 2026.

Additional references are documented in the Review 1 and Review 2
presentations. Bibliographic details and dataset licences should be
verified before final academic submission.

## 16. Project Documentation

The following supporting documents are maintained in the `docs/`
directory:

-   **Review 1:** Initial problem formulation, background study,
    research gap, proposed pipeline and novelty claims.
-   **Review 2:** Updated scope, panel feedback incorporation, extended
    literature survey, requirements, architecture, task allocation and
    evaluation strategy.
-   **Literature Survey Report:** Detailed research background and
    supporting literature.

------------------------------------------------------------------------

**Institution:** PES University\
**Department:** Computer Science and Engineering -- Artificial
Intelligence and Machine Learning\
**Project ID:** PW26_VK_02\
**Project Guide:** Dr. Vidhya K

*An academic capstone project developed as part of the B.Tech CSE (AI &
ML) programme, 2024--2028.*
