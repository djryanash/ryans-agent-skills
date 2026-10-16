---
name: brand-guidelines
description: Apply project or company brand guidelines (colors, typography, logo placement, and document formatting) to generated presentations, documents, and marketing assets. Use when styling external-facing materials or reports.
---

## Overview
This Skill ensures all generated presentations, documents, and visual assets adhere strictly to the target project or client brand identity. 

## Workflow

1. **Check for Brand Configuration**
   - Look for a `brand.json`, `.brandrc`, or `BRAND.md` file in the root workspace directory.
   - If present, parse the primary/secondary/accent hex codes, header/body font requirements, logo paths, and spacing rules.

2. **Prompt for Missing Guidelines**
   - If no brand configuration file exists in the repository, ask the user to provide:
     - Company/Brand Name
     - Primary, Secondary, and Accent Hex Colors
     - Header and Body Fonts
     - Logo location or usage preferences
   - *Optionally offer to run the `brand-setup` skill to save these preferences permanently.*

3. **Apply Standards During Asset Generation**
   - **Colors**: Use primary palette for focal points/headers, secondary for backgrounds/borders, and accent sparingly for callouts/CTAs.
   - **Typography**: Apply specified primary fonts for titles/headings and secondary body fonts for paragraphs and lists. Maintain consistent hierarchy and sizing.
   - **Logos**: Respect minimum clear-space margins, and select dark/light logo variants based on background contrast.

## Supported File Outputs
- Presentations (`.pptx`, Keynote)
- Documents (`.docx`, Markdown, PDF)
- HTML/CSS marketing components and email templates