
# Module 1: Introduction to LLMs

---

## 1. 环境依赖安装

使用以下命令安装所需的 Python 包：

```bash
pip install tqdm notebook==7.1.2 openai elasticsearch pandas scikit-learn ipywidgets
```

启动 Jupyter Notebook：

```bash
jupyter notebook
```

---

## 2. 通义千问模型使用

参考博客：[通义千问模型使用教程](https://blog.csdn.net/Rysxt_/article/details/149707413)

安装相关依赖：

```bash
pip install openai python-dotenv dashscope
```

### 配置环境变量

```bash
# 请将 API KEY 替换为你自己的
export OPENAI_API_KEY="sk-1c7c8651e8464b64b1b84ca3f182682d"
```

---

## 3. DashScope 原生模式示例

以下代码演示如何调用 DashScope API：

```python
import os
from openai import OpenAI

# 初始化 OpenAI 客户端
client = OpenAI(
        api_key=os.getenv("DASHSCOPE_API_KEY"),
        base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)

# 创建对话
completion = client.chat.completions.create(
        model="qwen-plus",  # 模型名称
        messages=[
                {"role": "system", "content": "你是一个专业的AI助手"},
                {"role": "user", "content": "你好，请自我介绍"}
        ],
        stream=False  # 是否流式输出
)

print(completion.choices[0].message.content)
```

---

## 4. 安装 Miniconda

下载并安装 Miniconda：

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-py310_25.5.1-1-Linux-x86_64.sh
bash Miniconda3-py310_25.5.1-1-Linux-x86_64.sh
```

---

## 5. 安装 Elasticsearch

```bash
pip install elasticsearch==8.10.1
```

使用 Docker 启动 Elasticsearch 服务：

```bash
docker run -it \
        --rm \
        --name elasticsearch \
        -p 9200:9200 \
        -p 9300:9300 \
        -e "discovery.type=single-node" \
        -e "xpack.security.enabled=false" \
        docker.elastic.co/elasticsearch/elasticsearch:8.4.3
```

---

## 6. Elasticsearch 索引设置

示例索引配置：

```json
{
    "settings": {
        "number_of_shards": 1,
        "number_of_replicas": 0
    },
    "mappings": {
        "properties": {
            "text":    {"type": "text"},
            "section": {"type": "text"},
            "question": {"type": "text"},
            "course":  {"type": "keyword"}
        }
    }
}
```

---

## 7. Elasticsearch 查询示例

```json
{
    "size": 5,
    "query": {
        "bool": {
            "must": {
                "multi_match": {
                    "query": "<your_query>",
                    "fields": ["question^3", "text", "section"],
                    "type": "best_fields"
                }
            },
            "filter": {
                "term": {
                    "course": "data-engineering-zoomcamp"
                }
            }
        }
    }
}
```

---

> **注释说明**：
> - 每个代码块前有简要说明。
> - 所有命令和配置均为原始内容，格式优化便于阅读和复制。
> - 请根据实际情况替换 API KEY 和查询内容。