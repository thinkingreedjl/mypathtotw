# Technical Writer · 能力·知识·技能·工具·资源清单

> 本清单每半年至少评审一次，根据主流工具链和社区实践进行更新。
> 设计逻辑：**能力为核心 → 知识打底 → 技能落地 → 工具支撑 → 资源随附**

---

## 核心胜任力（Core Competencies）

### 用户导向的技术文档设计与交付能力  
   说明：根据用户角色和任务场景（用户旅程/任务旅程）设计文档结构和导航，而非按功能模块堆砌。  
   资源：
   - https://www.writethedocs.org/guide/audience/
   - https://www.writethedocs.org/guide/oftware-documentation/
   - https://www.writethedocs.org/guide/index.html
   - https://resources.tcblabber.cn/  

### 复杂技术信息理解、简化、转化能力  
   说明：能从代码注释、设计文档、需求规格中提炼文档要点，而非仅依赖口头对齐。  
   资源：
   - https://developers.google.com/tech-writing  

### 信息架构（IA）与结构化内容组织能力  
   说明：掌握导航设计、面包屑、标签体系、内容分类等具体信息架构技能。  
   资源：
   - https://www.writethedocs.org/guide/information-architecture/
   - https://idratherbewriting.com/2020/02/25/information-architecture-for-docs/  

### 文档工程、质量控制与可测试性保障能力  
   说明：能配置 CI/CD 中的文档检查流水线（lint、链接检查、Vale）；能编写文档测试用例、对步骤类文档进行逐条验证，并建立文档质量检查清单。  
   资源：
   - https://www.writethedocs.org/guide/testing/
   - https://www.writethedocs.org/guide/tools/testing.html  

### 跨团队沟通、信息挖掘与推动评审能力  
   说明：能发起评审会、需求澄清会，高效向研发提问，推动确认与闭环；能设计并落地文档评审流程（自评 → 同行评审 → 研发评审 → 发布），明确评审角色与检查项。  
   资源：
   - https://developers.google.com/tech-writing/one
   - https://www.writethedocs.org/guide/communication/
   - https://idratherbewriting.com/learnapidoc/docapis_review_processes.html  

### 多语言、规范化、可维护内容创作能力  
   说明：能制定与维护团队风格指南，掌握中英日多语言内容维护流程。  
   资源：
   - https://developers.google.com/style
   - https://developers.google.com/tech-writing/creating-maintainable-documentation
   - https://learn.microsoft.com/en-us/style-guide/
   - https://learn.microsoft.com/ja/style-guide/  

### 作品集独立构建能力  
   说明：能用 MkDocs / Docusaurus / VitePress 搭建作品集并部署到 GitHub Pages / Netlify / Vercel。  
   资源：
   - https://www.writethedocs.org/guide/getting-a-job/portfolios/  

### 文档效果度量与数据驱动优化能力  
   说明：能通过搜索日志、停留时间、反馈数据等度量文档效果，并据此制定迭代策略。  
   资源：
   - https://www.writethedocs.org/guide/measuring-documentation-effectiveness/

---

## 必备知识体系（Knowledge）

### 技术写作核心原则（用户任务、清晰准确、可复现、完整）  
   资源：
   - https://developers.google.com/tech-writing  

### Diátaxis 文档框架与四大文档类型（Tutorial/How-To/Concept/Reference）  
   说明：按学习/行动/理解/参考四象限选择写作策略。  
   资源：
   - https://diataxis.fr/
   - https://www.writethedocs.org/guide/types/
   - https://blog.csdn.net/gitblog_00763/article/details/142837774  

### 文档全生命周期（需求→写作→评审→发布→维护→废弃）  
   说明：了解文档开发生命周期（DDLC）各阶段任务：需求分析、规划、撰写、评审、发布、维护、评估与废弃。  
   资源：
   - https://www.writethedocs.org/guide/lifecycle/
   - https://clickhelp.com/clickhelp-technical-writing-blog/document-development-life-cycle-ddlc-for-technical-writers/  

### 结构化写作、单源发布与内容复用（DITA/Markdown/conref/条件文本）  
   说明：能判断场景选择 DITA/XML 或 Markdown+SSG。  
   资源：
   - https://www.oasis-open.org/committees/dita/
   - https://www.markdownguide.org/  

### 术语管理、风格指南与一致性规范  
   说明：维护术语库、禁用词与过时术语清单，确保全文档统一。  
   资源：
   - https://github.com/sparanoid/chinese-copywriting-guidelines
   - https://www.ibm.com/docs/en/ibm-style-guide  

### 通用技术基础知识（OS/网络/API/数据格式/代码阅读/日志与监控）  
   - OS：Windows / Linux 命令、路径、权限、环境变量
   - 网络：HTTP/HTTPS、IP、端口、状态码
   - 数据格式：JSON/YAML/XML/INI
   - API：REST、OpenAPI、请求/响应/错误码
   - 代码阅读：Python/Java/JS 示例理解与注释
   - 日志：基础报错识别，支撑 Troubleshooting  
   资源：
   - https://developer.mozilla.org/zh-CN/docs/Learn
   - https://www.runoob.com/

### Docs as Code 与文档工程化理念  
   说明：分支策略、PR 模板、自动构建、预览与发布流程。  
   资源：
   - https://www.writethedocs.org/guide/docs-as-code/
   - https://git-scm.com/book/zh/v2  

### 本地化与国际化（l10n/i18n）基础  
   说明：ICU 格式、字符串长度、文化禁忌、多语言同步机制。  
   资源：
   - https://www.writethedocs.org/guide/localization/  

### 文档质量检查与评审体系  
   说明：质量清单 + 自测 + 同行评审 + 研发评审 + 自动化检查。  
   资源：
   - https://www.writethedocs.org/guide/reviewing/
   - https://resources.tcblabber.cn/  

### 可访问性（A11y）与 WCAG 核心原则及文档实践  
    资源：
    - https://w3c.github.io/WCAG21-zh/
    - https://www.w3.org/WAI/  

### 行业标准初探（DITA、S1000D）  
    说明：了解 DITA 在结构化写作中的角色，以及 S1000D 在航空航天/国防等高合规行业的典型应用场景。  
    资源：
    - https://www.s1000d.org/
    - https://www.oasis-open.org/committees/dita/

---

## 关键实操技能（Skills）

### 文档结构策划、目录设计与多层级导航优化  
   说明：能设计侧边栏导航、面包屑、页内目录、标签/分类体系，适配不同文档站点（SSG）。  
   资源：
   - https://www.writethedocs.org/guide/structure/  

### 标准化、可复现技术写作（步骤、前提、结果、异常、预期输出）  
   资源：
   - https://developers.google.com/tech-writing  

### 技术插图、流程图、架构图制作与视觉风格统一  
   资源：
   - https://app.diagrams.net/
   - https://www.figma.com/  

### 代码示例整理、最小可运行示例、注释与排版规范  
   资源：
   - https://developers.google.com/tech-writing/code  

### API 文档撰写（参数、请求、响应、错误码）与 OpenAPI 应用  
   说明：能从 Swagger/OpenAPI 提取信息并使用 Redoc/Swagger UI 渲染；理解文档驱动设计（documentation-driven design），在 API 设计时同步撰写文档。  
   资源：
   - https://spec.openapis.org/oas/latest.html
   - https://redocly.com/docs/redoc/
   - https://www.writethedocs.org/guide/writing/style-guides.html  

### 文档自测、可复现验证与人工测试  
   资源：
   - https://www.writethedocs.org/guide/testing/  

### 文档测试自动化与 CI/CD 流水线集成  
   资源：
   - https://www.docslikecode.com/book/testable-documentation.html  

### 结构化内容模型设计、复用与实施  
   资源：
   - https://www.oasis-open.org/committees/dita/  

### 评审执行、反馈处理、修订闭环与 PR 检查清单  
    资源：
   - https://resources.tcblabber.cn/  

### Git 版本控制、PR 协作、冲突处理与自动发布部署  
    资源：
    - https://docs.github.com/zh/getting-started  

### 风格检查、链接校验、格式规范化（Vale、markdownlint、Prettier）  
    资源：
    - https://vale.sh/
    - https://github.com/DavidAnson/markdownlint  

### 多语言术语统一、本地化协作与翻译配合  
    资源：
    - https://www.writethedocs.org/guide/localization/  

### 故障排查（Troubleshooting）与 FAQ 文档撰写  
    说明：能按“问题 → 现象 → 原因 → 解决方案 → 预防措施”结构编写 Troubleshooting 文档。  
    资源：
    - https://www.writethedocs.org/guide/troubleshooting/
    - https://www.writethedocs.org/videos/prague/2018/it-s-a-feature-documenting-known-issues-and-product-shortcomings-ivana-devcic.html  

### 文档版本管理、产品版本对齐与废弃文档策略  
    资源：
    - https://www.writethedocs.org/guide/lifecycle/maintenance/

---

## 工具与平台（Tools）

### 创作与专业编辑器  
- VS Code：https://code.visualstudio.com/
- Cursor：https://cursor.sh/
- Adobe FrameMaker：https://www.adobe.com/products/framemaker.html
- Oxygen XML Editor：https://www.oxygenxml.com/
- MadCap Flare：https://www.madcapsoftware.com/products/flare/

### AI 辅助写作工具  
- GitHub Copilot：https://github.com/features/copilot
- ChatGPT / Claude：https://chat.openai.com/
- 豆包：https://www.doubao.com/

### 静态站点生成器 SSG  
- MkDocs：https://www.mkdocs.org/
- MkDocs Material：https://squidfunk.github.io/mkdocs-material/
- Docusaurus：https://docusaurus.io/
- VitePress：https://vitepress.dev/
- Hugo：https://gohugo.io/
- Jekyll：https://jekyllrb.com/
- Sphinx：https://www.sphinx-doc.org/  

资源（选型对比）：
- https://www.writethedocs.org/guide/choosing-tools.html

### 协作与知识库平台
- Confluence：https://www.atlassian.com/software/confluence
- Notion：https://www.notion.so/
- 飞书文档：https://www.feishu.cn/doc/
- 腾讯文档：https://docs.qq.com/
- Baklib：https://www.baklib.com/

### API 文档工具链
- Swagger UI：https://swagger.io/tools/swagger-ui/
- Redoc：https://redocly.com/redoc/
- Stoplight：https://stoplight.io/
- Postman API Documentation：https://www.postman.com/api-documentation-tool/
- Doxygen：https://www.doxygen.nl/
- OpenAPI Generator：https://openapi-generator.tech/

### 绘图、可视化与多媒体
- draw.io (Diagrams.net)：https://app.diagrams.net/
- Excalidraw：https://excalidraw.com/
- Figma：https://www.figma.com/
- Mermaid：https://mermaid.js.org/
- PlantUML：https://plantuml.com/
- SnagIt：https://www.techsmith.com/snagit.html
- Greenshot：https://getgreenshot.org/
- ShareX：https://www.getsharex.com/
- SnipSVG：https://snipsvg.com/
- Camtasia：https://www.techsmith.com/camtasia.html
- ScreenToGif：https://www.screentogif.com/
- Loom：https://www.loom.com/

资源（图标库）：
- Material Design Icons：https://fonts.google.com/icons

### 语言、翻译与润色
- Grammarly：https://www.grammarly.com/
- LanguageTool：https://languagetool.org/
- DeepL：https://www.deepl.com/
- SDL Trados：https://www.rws.com/trados/
- MemoQ：https://www.memoq.com/

### 自动化、效率与质量检查
- AutoHotkey：https://www.autohotkey.com/
- PhraseExpress：https://www.phraseexpress.com/
- Vale：https://vale.sh/
- Prettier：https://prettier.io/
- markdownlint：https://github.com/DavidAnson/markdownlint
- markdown-link-check：https://github.com/tcort/markdown-link-check

### 托管与发布平台
- GitHub Pages：https://pages.github.com/
- Netlify：https://www.netlify.com/
- Vercel：https://vercel.com/
- Read the Docs（开源/社区版）：https://docs.readthedocs.com/platform/stable/index.html
- Read the Docs（企业版）：https://about.readthedocs.com/

---

## 权威资源索引（Resources）

### 官方风格指南（中/英/日）
- Google Developer Style Guide：https://developers.google.com/style
- Microsoft Style Guide（EN）：https://learn.microsoft.com/en-us/style-guide/
- Microsoft Style Guide（JA）：https://learn.microsoft.com/ja/style-guide/
- Apple Style Guide：https://developer.apple.com/style-guide/
- IBM Style Guide：https://www.ibm.com/docs/en/ibm-style-guide
- 中文文案排版指南：https://github.com/sparanoid/chinese-copywriting-guidelines
- JTF 日本翻訳連盟（日文技术文档参考）：https://www.jtf.jp/
- Write the Docs 风格指南聚合页：https://www.writethedocs.org/guide/writing/style-guides.html

### 标准与规范
- OpenAPI 3.0/3.1：https://spec.openapis.org/oas/latest.html
- WCAG 2.1：https://www.w3.org/TR/WCAG21/
- DITA Standard：https://www.oasis-open.org/committees/dita/
- S1000D：https://www.s1000d.org/

### 核心课程与学习资料
- Google Technical Writing：https://developers.google.com/tech-writing
- Write the Docs Guide：https://www.writethedocs.org/guide/

### 社区与行业组织
- Write the Docs：https://www.writethedocs.org/
- 技术传播共同体（CTCA）：http://www.china-tca.com/
- Awesome Technical Communication：https://github.com/lilin90/awesome-technical-communication

### 标杆文档参考
- 阿里云文档：https://help.aliyun.com/
- 腾讯云文档：https://cloud.tencent.com/document
- 华为云文档：https://support.huaweicloud.com/
- Docker 官方文档：https://docs.docker.com/
- Kubernetes 官方文档：https://kubernetes.io/docs/home/
- Stripe 官方文档：https://docs.stripe.com/