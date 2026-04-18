# Relational Database Schema Design – Learning Platform

## Overview
This project designs a fully normalized relational database schema for a learning management platform that organizes educational content, lessons, and media assets.

The system models how structured learning content is created, linked, and delivered using a scalable relational architecture.

---

## Problem
Educational content platforms need to manage:
- Structured learning units and lessons
- Media assets (videos, slides, etc.)
- Author ownership
- Reusable content across lessons

Without proper design, this leads to:
- Data redundancy
- Poor scalability
- Inconsistent relationships between content and assets

---

## Solution
This project implements a normalized relational schema that:
- Structures content into units and lessons
- Supports reusable learning assets across multiple lessons
- Maintains referential integrity across all entities
- Uses proper relational modeling techniques (1:M, M:N, 1:1, inheritance)

---

## Entity Relationship Model

The system is built using Crow’s Foot notation to define entity relationships and constraints.

📌 The ER diagram (page 1) shows:
- Hierarchical structure: LearningUnit → Lesson → Memo
- Many-to-many relationship between lessons and assets
- Inheritance structure for different asset types :contentReference[oaicite:0]{index=0}

---

## Core Entities

- **LearningUnit** – High-level course grouping
- **Lesson** – Individual instructional unit
- **Memo** – Supplementary lesson content (1:1 relationship)
- **LearningAsset** – Reusable content (videos, slides, etc.)
- **Author** – Creator of learning assets
- **Video / SlideDeck** – Specialized asset types

---

## Key Relationships

### One-to-Many (1:M)
- LearningUnit → Lesson  
- Author → LearningAsset  

### One-to-One (1:1)
- Lesson → Memo  
Each lesson has exactly one memo, enforced via a unique constraint :contentReference[oaicite:1]{index=1}  

### Many-to-Many (M:N)
- Lesson ↔ LearningAsset  
Implemented via a junction table:

```sql
LessonAsset(lessonID, assetID)
