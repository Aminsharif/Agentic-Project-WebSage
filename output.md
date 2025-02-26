[Phidata home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/phidata/logo/light.svg)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/phidata/logo/dark.svg)](https://docs.phidata.com/</>)
Search or ask...
Ctrl K
  * [Discord](https://docs.phidata.com/<https:/phidata.link/discord>)
  * [Community](https://docs.phidata.com/<https:/community.phidata.com/>)
  * [Log In](https://docs.phidata.com/<https:/phidata.app>)
  * [agno-agi/phidata](https://docs.phidata.com/<https:/github.com/agno-agi/phidata>)
  * [agno-agi/phidata](https://docs.phidata.com/<https:/github.com/agno-agi/phidata>)


Search...
Navigation
Getting Started
Introduction
[Documentation](https://docs.phidata.com/</introduction>)[Examples](https://docs.phidata.com/</examples/introduction>)[Templates](https://docs.phidata.com/</templates/introduction>)[Product Updates](https://docs.phidata.com/</changelog/overview>)[Reference](https://docs.phidata.com/</reference/agent>)[FAQs](https://docs.phidata.com/</faq/could-not-connect-to-docker>)
[Phidata home page![light logo](https://mintlify.s3.us-west-1.amazonaws.com/phidata/logo/light.svg)![dark logo](https://mintlify.s3.us-west-1.amazonaws.com/phidata/logo/dark.svg)](https://docs.phidata.com/</>)
##### Getting Started
  * [Introduction](https://docs.phidata.com/</introduction>)
  * [Agent UI](https://docs.phidata.com/</agent-ui>)
  * [Examples](https://docs.phidata.com/</more-examples>)
  * [Monitoring](https://docs.phidata.com/</monitoring>)
  * [Workflows](https://docs.phidata.com/</workflows>)
  * [Getting Help](https://docs.phidata.com/</getting-help>)


##### Documentation
  * Agents
  * Models
  * Tools
  * Knowledge
  * Chunking
  * VectorDbs
  * Storage
  * Embeddings
  * Workflows


##### How To
  * [Install & Upgrade](https://docs.phidata.com/</how-to/install>)
  * [Upgrade to v2.5.0](https://docs.phidata.com/</migration/2-5-0>)


Getting Started
# Introduction
**Build agents and workflows to automate intelligent work.**
Phidata is now Agno! We’ve moved! Check out our new home at [Agno AGI](https://docs.phidata.com/<https:/github.com/agno-agi/agno>)
## 
[​](https://docs.phidata.com/<#what-is-phidata%3F>)
What is Phidata?
**Phidata is a framework for building multi-modal agents and workflows.**
  * **Build agents with memory, knowledge, tools and reasoning.**
  * **Build teams of agents that can work together to solve problems.**
  * **Interact with your agents and workflows using a beautiful Agent UI.**


## 
[​](https://docs.phidata.com/<#key-features>)
Key Features
  * [Simple & Elegant](https://docs.phidata.com/</introduction#simple-and-elegant>)
  * [Powerful & Flexible](https://docs.phidata.com/</introduction#powerful-and-flexible>)
  * [Multi-Modal by default](https://docs.phidata.com/</introduction#multi-modal-by-default>)
  * [Multi-Agent orchestration](https://docs.phidata.com/</introduction#multi-agent-orchestration>)
  * [A beautiful Agent UI to chat with your agents](https://docs.phidata.com/</agent-ui>)
  * [Agentic RAG built-in](https://docs.phidata.com/</more-examples#agentic-rag>)
  * [Structured outputs](https://docs.phidata.com/</more-examples#structured-outputs>)
  * [Reasoning built-in](https://docs.phidata.com/</more-examples#reasoning-agent>)
  * [Monitoring & Debugging built-in](https://docs.phidata.com/</monitoring>)


## 
[​](https://docs.phidata.com/<#install>)
Install
Copy
```
pip install -U phidata

```

## 
[​](https://docs.phidata.com/<#simple-%26-elegant>)
Simple & Elegant
Phidata Agents are simple and elegant, resulting in minimal, beautiful code.
For example, you can create a web search agent in 10 lines of code.
web_search.py
Copy
```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.duckduckgo import DuckDuckGo
web_agent = Agent(
  name="Web Agent",
  model=OpenAIChat(id="gpt-4o"),
  tools=[DuckDuckGo()],
  instructions=["Always include sources"],
  show_tool_calls=True,
  markdown=True,
)
web_agent.print_response("Tell me about OpenAI Sora?", stream=True)

```

### 
[​](https://docs.phidata.com/<#setup>)
Setup
1
Setup your virtual environment
Mac
Windows
Copy
```
python3 -m venv ~/.venvs/aienv
source ~/.venvs/aienv/bin/activate

```

2
Install libraries
Mac
Windows
Copy
```
pip install -U phidata openai duckduckgo-search

```

3
Export your OpenAI key
Phidata works with most model providers but for these examples let’s use OpenAI.
Mac
Windows
Copy
```
export OPENAI_API_KEY=sk-***

```

You can get an API key from [here](https://docs.phidata.com/<https:/platform.openai.com/account/api-keys>).
4
Run the agent
Copy
```
python web_search.py

```

## 
[​](https://docs.phidata.com/<#powerful-%26-flexible>)
Powerful & Flexible
Phidata agents can use multiple tools and follow instructions to achieve complex tasks.
For example, you can create a finance agent with tools to query financial data.
1
Create a finance agent
finance_agent.py
Copy
```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.yfinance import YFinanceTools
finance_agent = Agent(
  name="Finance Agent",
  model=OpenAIChat(id="gpt-4o"),
  tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, company_info=True, company_news=True)],
  instructions=["Use tables to display data"],
  show_tool_calls=True,
  markdown=True,
)
finance_agent.print_response("Summarize analyst recommendations for NVDA", stream=True)

```

2
Run the agent
Install libraries
Copy
```
pip install yfinance

```

Run the agent
Copy
```
python finance_agent.py

```

## 
[​](https://docs.phidata.com/<#multi-modal-by-default>)
Multi-Modal by default
Phidata agents support text, images, audio and video.
For example, you can create an image agent that can understand images and make tool calls as needed
1
Create an image agent
image_agent.py
Copy
```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.duckduckgo import DuckDuckGo
agent = Agent(
  model=OpenAIChat(id="gpt-4o"),
  tools=[DuckDuckGo()],
  markdown=True,
)
agent.print_response(
  "Tell me about this image and give me the latest news about it.",
  images=["https://upload.wikimedia.org/wikipedia/commons/b/bf/Krakow_-_Kosciol_Mariacki.jpg"],
  stream=True,
)

```

2
Run the agent
Copy
```
python image_agent.py

```

## 
[​](https://docs.phidata.com/<#multi-agent-orchestration>)
Multi-Agent orchestration
Phidata agents can work together as a team to achieve complex tasks.
1
Create an agent team
agent_team.py
Copy
```
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.tools.duckduckgo import DuckDuckGo
from phi.tools.yfinance import YFinanceTools
web_agent = Agent(
  name="Web Agent",
  role="Search the web for information",
  model=OpenAIChat(id="gpt-4o"),
  tools=[DuckDuckGo()],
  instructions=["Always include sources"],
  show_tool_calls=True,
  markdown=True,
)
finance_agent = Agent(
  name="Finance Agent",
  role="Get financial data",
  model=OpenAIChat(id="gpt-4o"),
  tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, company_info=True)],
  instructions=["Use tables to display data"],
  show_tool_calls=True,
  markdown=True,
)
agent_team = Agent(
  team=[web_agent, finance_agent],
  instructions=["Always include sources", "Use tables to display data"],
  show_tool_calls=True,
  markdown=True,
)
agent_team.print_response("Summarize analyst recommendations and share the latest news for NVDA", stream=True)

```

2
Run the agent team
Run the agent team
Copy
```
python agent_team.py

```

## 
[​](https://docs.phidata.com/<#continue-reading>)
Continue reading
  * Chat with your Agents using a beautiful [Agent UI](https://docs.phidata.com/</agent-ui>).
  * [More examples](https://docs.phidata.com/</more-examples>)
  * [Monitoring & Debugging](https://docs.phidata.com/</monitoring>)


Was this page helpful?
YesNo
[Suggest edits](https://docs.phidata.com/<https:/github.com/agno-agi/phidata-docs/edit/main/introduction.mdx>)
[Agent UI](https://docs.phidata.com/</agent-ui>)
[x](https://docs.phidata.com/<https:/x.com/phidatahq>)[github](https://docs.phidata.com/<https:/github.com/agno-agi/phidata>)[discord](https://docs.phidata.com/<https:/phidata.link/discord>)[youtube](https://docs.phidata.com/<https:/phidata.link/youtube>)[website](https://docs.phidata.com/<https:/phidata.com>)
[Powered by Mintlify](https://docs.phidata.com/<https:/mintlify.com/preview-request?utm_campaign=poweredBy&utm_medium=docs&utm_source=docs.phidata.com>)
On this page
  * [What is Phidata?](https://docs.phidata.com/<#what-is-phidata%3F>)
  * [Key Features](https://docs.phidata.com/<#key-features>)
  * [Install](https://docs.phidata.com/<#install>)
  * [Simple & Elegant](https://docs.phidata.com/<#simple-%26-elegant>)
  * [Setup](https://docs.phidata.com/<#setup>)
  * [Powerful & Flexible](https://docs.phidata.com/<#powerful-%26-flexible>)
  * [Multi-Modal by default](https://docs.phidata.com/<#multi-modal-by-default>)
  * [Multi-Agent orchestration](https://docs.phidata.com/<#multi-agent-orchestration>)
  * [Continue reading](https://docs.phidata.com/<#continue-reading>)


