# UserStoryAgent

**A Criterion-Level Multi-Agent Framework for User Story Quality Assessment and Rewriting**

UserStoryAgent is a multi-agent workflow implemented in [Dify](https://dify.ai/) for verification-oriented quality assessment and targeted rewriting of individual user stories and their acceptance criteria. Seven criterion-specific Validator Agents assess a user story and produce explanations of identified violations. A Rewriter Agent then uses the aggregated feedback and retrieved knowledge to generate criterion-aligned revisions.

The framework is described in the research paper *Decouple, Ground, and Verify: A Criterion-Level Multi-Agent Framework for Auditable User Story Quality Assurance*.

## 1. Repository Contents

- **`validator-rewriter.yml`** — The Dify workflow configuration for the Validator–Rewriter framework. It contains the agent prompts, processing logic, retrieval nodes, and workflow connections.
- **`upload_wiki/`** — A **de-identified example** of the project Wiki knowledge base described in the paper. Project-sensitive information has been anonymized. These files are provided to illustrate Wiki-based grounding and are not the original, unmodified industrial Wiki.

**Note:** The **rewriting-case knowledge base is not included** in the repository and must be created separately. It can be populated with previously reviewed rewriting examples that record the violated quality criterion, reason for violation, original user story, and corresponding compliant rewrite(s).

## 2. Workflow Overview

The workflow follows four main stages:

1. **Input preprocessing:** Extract the user-story statement, acceptance criteria, and supplementary background from the input text.
2. **Quality assessment:** Seven Validator Agents independently assess **Well-formed, Minimal, Atomic, Unambiguous, Conceptually Sound, Problem-oriented, and Internal Consistency**. Each provides a violation decision and a corresponding explanation.
3. **Feedback aggregation:** Combine the criterion-level findings into a quality assessment report.
4. **Knowledge-supported rewriting:** When violations are detected, retrieve relevant rewriting cases and Wiki passages from two Dify knowledge bases. The Rewriter Agent uses the aggregated feedback and retrieved context to revise the story, guided by a prompt-embedded Fact Checklist.

## 3. Installation and Configuration

### Step 1. Import the workflow into Dify

1. Open [Dify](https://dify.ai/) and sign in to your workspace.
2. Go to **Studio (工作室)** and create an application by importing a **DSL/YAML** file.
3. Select `validator-rewriter.yml` from this repository and import it as a Workflow application.
4. Open the imported workflow and configure the required model provider and API credentials in your Dify workspace. Check that the models used by its LLM nodes are available.

For additional guidance on workflow import and model configuration, see the [Dify documentation](https://docs.dify.ai/).

### Step 2. Create the two knowledge bases in Dify

In Dify, go to **Knowledge (知识)** and create **two separate knowledge bases**:

**A. Project Wiki knowledge base**

1. Create a new knowledge base in **Knowledge**.
2. Upload the de-identified example documents from `upload_wiki/`.
3. Complete document processing and indexing in Dify. Configure the retrieval settings according to the paper or your application needs.

**B. Rewriting-case knowledge base**

1. Create another knowledge base in **Knowledge**.
2. Prepare and upload your **own rewriting-case records**. Each record should include the violated criterion, violation reason, original user story, and one or more compliant rewritten versions.
3. Complete document processing and indexing in Dify, and configure the retrieval settings.

The Wiki examples are supplied for demonstration only. The rewriting-case records must be prepared by the user; neither knowledge base is automatically recreated by importing the workflow YAML.

### Step 3. Bind the knowledge bases to the workflow

1. Return to the imported application in **Studio** and open its workflow editor.
2. Select the knowledge-retrieval node **`Wiki检索`** and choose the Project Wiki knowledge base created in Step 2.
3. Select **`检索改写案例`** and choose the Rewriting-case knowledge base created in Step 2.
4. Confirm the retrieval configurations and save the workflow.
5. Use Dify's **Debug/Run (调试/运行)** function to check whether the model calls and both knowledge-retrieval nodes work as expected.

**Important:** The exported workflow stores knowledge-base references, but it does not include the indexed knowledge-base contents. The two knowledge bases must be created in Dify and explicitly selected in their respective retrieval nodes after import.

## 4. License

See the repository's `LICENSE` file for licensing terms. Dify, model services, and third-party data are subject to their respective terms.
