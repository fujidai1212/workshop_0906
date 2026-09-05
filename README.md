# workshop_0906

LLM エージェントのワークショップ用ノートブック（Google Colab 想定）。

「LLM エージェントとは LLM + ツール呼び出し + コンテキスト管理である」を、
**自分で書く回**と**フレームワークを使う回**の2本で確かめる構成になっている。

## ファイル

### `LLMAgent_Workshop.ipynb` — 第1回: フレームワークを使わずに作る

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/fujidai1212/workshop_0906/blob/main/LLMAgent_Workshop.ipynb)

OpenAI API だけを使い、エージェントの本体である while ループを素の Python で書く。
題材は社内ヘルプデスク（ツール7個 / KB24件・チケット16件・社員18名の自作 JSON）。

課題0〜7 で、`MAX_STEPS` を削る・トークン数を数える・システムプロンプトを1行消す・
ツールの `description` に嘘を書く、といった改造を通して挙動の変化を観察する。
最後の課題7 は**プロンプトインジェクション**で、汚染されたチケットを読ませると
エージェントが外部データの指示に従ってしまうことを実際に見る。

### `Travel_Agent_Workshop.ipynb` — 第2回: LangGraph で作る

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/fujidai1212/workshop_0906/blob/main/Travel_Agent_Workshop.ipynb)

第1回と同じ「ループ」を、今度は LangGraph の**グラフ**として組む。
題材は **AgentDojo の travel スイート**（旅行業務。ツール28個 / ユーザータスク20件 / 攻撃タスク7件）で、
第1回の7ツールでは出てこなかった規模の問題を扱う。

課題1 では単純なループではなくワークフローとしてグラフを設計し、
課題2 では汚染されたレビュー文を読ませてインジェクションを試す（攻撃文7種を収録）。

## 使い方

どちらも Colab で開き、**上のメニューから「ドライブにコピーを保存」**を押してから、
セルを**上から順に**実行する。OpenAI API キーが必要。

`%%writefile` の付いたセルは実行すると `.py` ファイルとして書き出され、
後続の `!python ...` セルがそれを動かす、という作りになっている。

## 出典

travel スイートのツール・データ・タスク文は AgentDojo (v0.1.23) から引用したもの。

> AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents
> ETH Zurich SPY Lab, NeurIPS 2024, [arXiv:2406.13352](https://arxiv.org/abs/2406.13352)
> [github.com/ethz-spylab/agentdojo](https://github.com/ethz-spylab/agentdojo) — MIT License
