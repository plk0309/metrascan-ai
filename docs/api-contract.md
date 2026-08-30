 # API Contract

Base URL: `/api/v1`

## POST /inspections
Create a new inspection.
**Response:** `{ "inspection_id": "INS_001", "status": "created" }`

## POST /inspections/{id}/images
Upload `front_image`, `back_image`, `mrp_image` (multipart/form-data).

## POST /inspections/{id}/analyze
Triggers ML analysis. Backend calls ml-service internally.

## GET /inspections/{id}
Returns full result:
```json
{
  "inspection_id": "INS_001",
  "overall_status": "NEEDS_MANUAL_CHECK",
  "fields": [
    { "name": "MRP", "value": "₹50", "confidence": 0.96, "status": "PASS" }
  ],
  "violations": [],
  "measurements": [],
  "manual_review_required": true
}
```

## GET /inspections/{id}/report
Returns the formatted compliance report.

## POST /inspections/{id}/verify
Officer submits decision: `{ "decision": "confirm" | "reject" | "manual_review" }`

---

## ML Service Contract (internal — backend ↔ ml-service)
**Request:** `{ "inspection_id": "INS_001", "images": ["url1", "url2"] }`
**Response:**
```json
{
  "status": "success",
  "ocr_results": [
    { "text": "MRP ₹50 inclusive of all taxes", "bbox": {"x":120,"y":300,"width":450,"height":40}, "confidence": 0.98 }
  ],
  "fields": [
    { "field_type": "mrp", "value": "₹50", "confidence": 0.95 }
  ]
}
```

## Status
🚧 Draft — freeze this before backend/ML development starts in parallel.
