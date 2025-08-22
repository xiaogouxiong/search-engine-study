
# Vector Search with Qdrant

## Reference Material
- [LLM Zoomcamp - Vector Search](https://github.com/DataTalksClub/llm-zoomcamp/blob/main/02-vector-search/sematic_search.ipynb)

## Installation Instructions

### Qdrant Client Installation

**普通终端:**
```bash
pip install -q "qdrant-client[fastembed]>=1.14.2"
```

**Jupyter Notebook:**
```python
!python -m pip install -q "qdrant-client[fastembed]>=1.14.2"
```

### Docker Setup
```bash
docker pull qdrant/qdrant

docker run -p 6333:6333 -p 6334:6334 \
   -v "$(pwd)/qdrant_storage:/qdrant/storage:z" \
   qdrant/qdrant
```

**Port Information:**
- Port 6333: REST API
- Port 6334: gRPC API

**Web Interface:**  
Access the Web UI at [http://localhost:6333/dashboard](http://localhost:6333/dashboard)

## Example Data Point
```json
// This is a simple point
{
    "id": 129,
    "vector": [0.1, 0.2, 0.3, 0.4],
    "payload": {"color": "red"},
}
```

## Additional Resources
- [FastEmbed Documentation](https://github.com/qdrant/fastembed)
- [What is a Vector Database?](https://qdrant.tech/articles/what-is-a-vector-database/)
- [Jina Embeddings Model](https://huggingface.co/jinaai/jina-embeddings-v2-small-en)
- [Qdrant Collections](https://qdrant.tech/documentation/concepts/collections/)
- [Vector Search Filtering](https://qdrant.tech/articles/vector-search-filtering/)
- [Points Documentation](https://qdrant.tech/documentation/concepts/points/#points)
- [Payload Indexing](https://qdrant.tech/documentation/concepts/indexing/#payload-index)
- [MCP Server Qdrant](https://github.com/qdrant/mcp-server-qdrant)