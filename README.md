# algo-hw11-vllm-prefix-cache
Algorithms HW11 - vLLM Prefix Caching Experiment
# Algorithms HW11 — vLLM Prefix Caching
## 學生資訊
- 姓名：[翁歆婷]
- 學號：[B3201673]
- 課程：3468 演算法 1142
## 實驗環境
- 平台：Google Colab T4
- vLLM 版本：0.21.0
- 模型：Qwen2.5-0.5B-Instruct（或你實際用的）
- prompts 數：100
- max_tokens：64
## 結果摘要
========== 比較摘要 ==========<br>
  吞吐 (req/s) 加速:  3.41 倍<br>
  吞吐 (tok/s) 加速:  3.41 倍<br>
  總耗時下降:          70.6%  (5.81s → 1.71s)<br>
  (TTFT 缺失:vLLM V1 engine 在 offline 模式不回傳 per-request metrics)
## 結論
本次測試中分別測試關閉跟開啟快取，其中開啟後每秒可處理的請求量跟token急速上升，高達58.6，相較尚未開啟快取的17.2快了高達3.41倍，符合應在範圍2~4倍內，因此總執行耗時下降70%，其中因vLLM版本過新，故沒看到TTFI的輸出，多次嘗試如安裝較舊版本，但是會跟其他檔案衝突之類的。

對應到§11.4 :vLLM 的 block hash 表 Dict[block_hash, PhysicalBlock] 使用Python的dict，其中block_hash是用SHA-256，使得碰撞機率極低，實務上不易發生，其中不採用 Universal Hashing 是因該方法應用於輸入可被惡意控制的情況。但在 vLLM 的使用中，SHA-256的方法使得其很難被惡意製造出碰撞，不太需用 Universal Hashing 。
## 對應作業
- 作業：3468 演算法 HW11 (Ch11) Problem 8(a)
- 投影片：CLRS 4e Ch11 v4 PPT 第 82 頁
- 實驗指南：本 repo 內 README-11-p76.md