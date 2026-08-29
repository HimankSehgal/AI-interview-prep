# Attentiv.ai — Research Engineer 🏗️

## Overview

Attentiv.ai is an AI-powered platform for construction and landscaping intelligence. They use satellite and aerial imagery to automate site monitoring, progress tracking, and analysis for construction projects. Backed by Peak XV (Sequoia Surge) and InfoEdge Ventures.

The interview is heavily focused on computer vision and practical ML engineering — makes sense given their core product is built on image analysis.

**Structure:** 4 rounds

| Round | Focus |
|---|---|
| Round 1 | Intro + Background |
| Round 2 | Coding |
| Round 3 | Projects + CV Deep Dive |
| Round 4 | Hiring Manager + System Design |

---

## 🔍 Round 1 — Intro (30 mins)

Short round. Very conversational.

- Walk through your background and work experience
- Why Attentiv? What interests you about their problem?
- Brief explanation of what Attentiv does — they will explain their product, ask clarifying questions to show genuine curiosity
- No technical questions in this round

💡 *Tip: Know what Attentiv does before going in. They use satellite imagery for construction site monitoring — understand the core problem they are solving.*

---

## 💻 Round 2 — Coding

Two Python questions.

### Question 1 — Number of Islands

**Problem:** Given a 2D grid of '1's (land) and '0's (water), count the number of islands.

**Approach:** BFS or DFS — traverse grid, when you find a '1', do DFS to mark all connected land as visited, increment island count.

```python
def num_islands(grid):
    if not grid:
        return 0
    
    count = 0
    
    def dfs(i, j):
        if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]):
            return
        if grid[i][j] != '1':
            return
        grid[i][j] = '0'  # mark as visited
        dfs(i+1, j)
        dfs(i-1, j)
        dfs(i, j+1)
        dfs(i, j-1)
    
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == '1':
                dfs(i, j)
                count += 1
    
    return count
```

LeetCode link: [LC 200 — Number of Islands](https://leetcode.com/problems/number-of-islands/)

### Question 2 — Implement Bubble Sort

**Problem:** Implement bubble sort from scratch.

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr
```

Time complexity: O(n²). Space: O(1).

💡 *Tip: For bubble sort, mention the optimisation — if no swap happens in a full pass, array is already sorted. You can add a flag to break early.*

---

## 🤖 Round 3 — Projects + Computer Vision Deep Dive

Deep dive into your CV projects. My Blinkit project was the main one discussed.

### Project Discussion (Blinkit — YOLO + Gemini)
- What was the problem you were solving?
- Walk through your pipeline end to end
- What model did you use and why?
- What were your metrics? What accuracy did you achieve?
- What challenges did you face? How did you solve them?

### YOLO Questions
- What is YOLO and what problem does it solve?
- What are bounding boxes?
- What is the math behind bounding box prediction?
  - Grid cells — image divided into S×S grid
  - Each cell predicts B bounding boxes: (x, y, w, h, confidence)
  - x, y: centre of box relative to grid cell
  - w, h: width and height relative to full image
  - Confidence: P(object) × IoU(pred, ground truth)
- What is IoU (Intersection over Union)?
- What is Non-Maximum Suppression (NMS)?
- Loss function: localisation loss + confidence loss + classification loss

### CNN Questions
- What is a CNN?
- What are the advantages of CNN over a traditional ANN?
  - Weight sharing — same filter applied across image, fewer parameters
  - Spatial hierarchy — learns edges → textures → shapes progressively
  - Translation invariance — recognises pattern regardless of location
- What are convolutional layers, pooling layers, and fully connected layers?

### GAN Questions
- What is a GAN?
- What are the two components — Generator and Discriminator?
- How do they train together? (minimax game)
- What is mode collapse and how do you deal with it?
- Applications — image generation, data augmentation, style transfer

---

## 🛰️ Round 4 — Hiring Manager + System Design

Hiring manager round with a system design question based on Attentiv's actual problem domain.

**Problem Statement:** Build an end-to-end ML pipeline for object detection in satellite/aerial imagery of construction sites.

### Full Pipeline Approach

**Step 1 — Problem Clarification**
- What objects to detect? (machinery, workers, materials, structures, vehicles)
- What resolution is the imagery? (affects model choice)
- Real-time or batch processing?
- What is the acceptable latency?
- What is the business metric? (site progress %, safety violations detected)

**Step 2 — Data Strategy**
- Collect satellite imagery at different time stamps
- Annotate bounding boxes for objects of interest
- Challenges specific to aerial imagery:
  - Small objects (workers, equipment look tiny from above)
  - Top-down perspective (different from standard CV datasets)
  - Lighting changes (shadows, time of day)
  - Occlusion (objects partially hidden by structures)
- Data augmentation: rotation, flipping, brightness changes, scale variations

**Step 3 — Baseline Model**
- Start with pretrained YOLO (YOLOv8) fine-tuned on aerial imagery
- COCO pretrained weights as starting point
- Establish baseline mAP on holdout set

**Step 4 — Model Selection & Improvements**
- For small objects: use multi-scale feature maps (FPN — Feature Pyramid Network)
- For high resolution imagery: tiling strategy — split image into overlapping tiles, run detection on each, merge results
- Consider: Faster R-CNN for higher accuracy when latency allows, YOLO for real-time

**Step 5 — Evaluation**
- Primary: mAP@0.5 IoU (standard object detection metric)
- Secondary: Precision and Recall per class
- Business: % of site progress correctly estimated, safety violation detection rate

**Step 6 — Deployment**
- Batch processing pipeline for daily/weekly satellite imagery ingestion
- FastAPI service for on-demand inference
- Model weights stored on S3, served via Docker container
- Monitoring: track mAP on held-out validation set over time

**Step 7 — Monitoring & Retraining**
- Monitor for data drift — new construction types, new equipment not seen in training
- Retrain trigger: mAP drops below threshold on recent validation data
- Active learning: flag low-confidence predictions for human review, add to training data

💡 *Tip: The key insight for aerial imagery is the small object problem. Mentioning multi-scale features and tiling strategy shows you understand the domain-specific challenges.*

---

## 🎯 Overall Takeaway

Attentiv is a focused CV company. They want people who understand computer vision deeply — not just LLMs and GenAI.

What to focus on:
- **YOLO** — bounding boxes, loss function, NMS, IoU — know the math
- **CNNs** — architecture, why they work for images, pooling, weight sharing
- **GANs** — generator/discriminator, training dynamics, mode collapse
- **Aerial imagery challenges** — small objects, top-down perspective, multi-scale detection
- **Basic DSA** — graphs (BFS/DFS), sorting algorithms

---

*🔙 [Back to main repo](./README.md)*
