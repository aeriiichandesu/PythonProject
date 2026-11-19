# 智扫通机器人智能客服

基于 Python、Streamlit、LangChain 和 Chroma 的扫地机器人智能客服项目，支持知识库问答和使用报告生成。

## 功能

- 从本地 PDF、TXT 知识库检索选购、故障排除和维护保养资料。
- 通过 DeepSeek 对话模型和 DashScope 嵌入模型生成回答。
- 使用 Agent 工具及动态提示词生成使用报告。
- 使用 Streamlit 展示聊天界面。

天气接口返回固定示例值，用户 ID、城市和月份使用随机选取，未连接真实天气或用户系统。

## 本地运行

使用 Python 3.10 或更高版本，在项目根目录执行：

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
```

在 `.env` 中填写自己的 `DEEPSEEK_API_KEY` 和 `DASHSCOPE_API_KEY`。模型名称见 `config/rag.yml`。模型调用需要联网，可能产生服务商费用。

首次运行先建立知识库，再启动界面：

```bash
python -m RAG.vector_store
streamlit run app.py
```

Windows 用户可使用 `.venv\Scripts\activate` 激活虚拟环境。请始终从项目根目录运行命令，确保向量数据库路径一致。

## 项目结构

```text
app.py             Streamlit 入口
agent/             Agent、工具和中间件
RAG/               文档入库、检索和回答
model/             对话与嵌入模型工厂
config/            YAML 配置
prompts/           提示词模板
data/              知识库资料及报告使用记录
utils/             配置、路径、日志和文件工具
```

## 发布说明

仓库不包含真实 API 密钥、虚拟环境、IDE 设置、运行日志和已生成的向量数据库。`.env.example` 仅含占位符。依赖版本来自原项目本地环境；本次发布未进行在线模型调用或完整运行验证。

删除向量数据库并重新构建时，也需删除本地 `md5.text`，否则已处理文档可能被跳过。
