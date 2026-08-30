 # MetraScan AI — System Architecture

## Pipeline Overview
Product photos → Image quality check → OCR (PaddleOCR) → Text + bounding boxes
→ Field detection (AI/regex) + Physical measurement (reference card) in parallel
→ Rule engine (YAML/JSON) → Compliance report → Officer verification

## Components
| Service      | Owner   | Tech                          |
|--------------|---------|--------------------------------|
| frontend     | Tarrush | React/Next.js, TypeScript, Tailwind |
| backend      | Aryan   | FastAPI, PostgreSQL, SQLAlchemy |
| ml-service   | Kartik  | PaddleOCR, OpenCV, YOLO, VLM  |
| rules        | Aryan   | YAML/JSON config              |
| integration  | Palak   | Docker, CI/CD, testing        |

## Data Flow
1. Frontend uploads 3 images (front, back, MRP+card) → Backend
2. Backend stores images, creates inspection record, calls ML service
3. ML service returns OCR + fields + measurements → Backend
4. Backend runs rule engine against ML output → generates report
5. Officer reviews report in frontend → confirms/rejects → Backend saves decision

## Status
🚧 Draft — update as contracts are finalized in Week 1.
