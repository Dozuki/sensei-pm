---
name: create-portal-card
description: Help Product Managers generate a productboard portal card from a PRD using Dozuki's standardized template, ensuring that all necessary information is included and formatted correctly for submission.
---

# Portal Card Creation
> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../../CONNECTORS.md).

Productboard portal cards are used to communicate the development of a feature to customers and stakeholders. This skill helps Product Managers generate a portal card from a PRD using Dozuki's standardized template, ensuring that all necessary information is included and formatted correctly for submission.

## Usage
```
/create-portal-card $ARGUMENTS
```

## Workflow 
### 1. Get the Product Requirements Document (PRD)
Accept the PRD in any of these forms:
   * Pasted text directly into the chat
   * A Notion link (if `~~knowledge base` is connected, fetch the document)
   * A file attachment

if no PRD is provided, ask the user to paste or share it before proceeding.

### 2. Extract information from PRD
   - Feature name
   - Description
   - Problem statement
   - Solution overview
   - Target audience
   - Benefits and value proposition

### 3. Create a Portal Card description
Use the template in `references/TEMPLATE.md` to structure the output. A complete hypothesis document fills every template section:
   - Overview
   - How it Works
   - Who's it For
   - Additional Information
