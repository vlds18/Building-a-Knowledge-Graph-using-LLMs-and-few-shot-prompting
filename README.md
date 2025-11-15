# PDF-based Knowledge Graph Construction with LLM and Neo4j

This repository implements an end-to-end pipeline for extracting structured knowledge from scientific PDF documents using Large Language Models (LLMs) and building interactive knowledge graphs with Neo4j integration.

## Project overview

The pipeline transforms unstructured PDF text into structured knowledge graphs through:

- PDF text extraction using PyPDF2
- Intelligent text chunking for optimal processing
- LLM-powered triple extraction using OpenAI GPT-4
- Knowledge graph visualization with PyVis
- Neo4j graph database integration for persistent storage

## Installation

```bash
pip install PyPDF2 pyvis tqdm neo4j
```
## Dependencies

- **PyPDF2**: PDF text extraction
- **pyvis**: Interactive graph visualization
- **tqdm**: Progress tracking
- **neo4j**: Graph database connectivity
- **openai**: LLM API integration
- **IPython**: Notebook display capabilities

## Pipeline structure

### 1. PDF Text Extraction
```python
with open(pdf_path, "rb") as f:
    reader = PyPDF2.PdfReader(f)
    for page in reader.pages:
        text += page.extract_text() + "\n"
```
### 2. Text chunking
Intelligent splitting of text into manageable chunks (400 tokens) while preserving sentence boundaries for optimal LLM processing.

### 3. LLM-Powered triple extraction
Using OpenAI GPT-4 to extract structured triples in (subject, relation, object) format with strict JSON output.

### 4. Data Cleaning and Normalization
- Removing whitespace and punctuation
- Filtering vague entities ("it", "this", "they")
- Ensuring meaningful subject-object pairs

### 5. Interactive visualization
Creating browser-based interactive knowledge graphs with PyVis, featuring:
- Color-coded nodes
- Relation-labeled edges
- Zoom and selection capabilities

### 6. Neo4j Integration
Persistent storage of extracted knowledge in graph database with Cypher queries.

## Key features

### LLM Extraction Prompt
Advanced prompt engineering to ensure consistent JSON output format and high-quality triple extraction.

### Neo4j Data Model

```python
(:Entity {name: string})-[:RELATION {type: string}]->(:Entity {name: string})
```

## Output

- **Interactive HTML Visualization**: `kg_llm.html`
- **Structured Triples**: List of (subject, relation, object) dictionaries
- **Neo4j Database**: Persistent graph storage with querying capabilities

## Example output
```json
[
  {"subject": "genes", "relation": "cause", "object": "oncogenesis"},
  {"subject": "cancer research", "relation": "aims to identify", "object": "genes that cause oncogenesis"},
  {"subject": "somatic mutations", "relation": "alter the function of", "object": "critical gene"}
]

## Security best practices

- Environment variables for API keys
- Secure credential handling
- No hard-coded sensitive information

## Performance

- Extracted 70 triples from genomics research paper
- Efficient chunking prevents token limits
- Batch processing for large documents

## Use cases

- Scientific literature mining
- Biomedical research knowledge extraction
- Academic paper analysis
- Domain-specific knowledge graph construction

## Future enhancements

- Multi-model LLM support
- Advanced entity resolution
- Relationship confidence scoring
- Temporal knowledge tracking
- Automated graph analytics
