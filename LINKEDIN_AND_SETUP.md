# LinkedIn post + how to get this on GitHub

---

## 📌 LinkedIn post (recruiter-facing, technical)

> Just shipped a portfolio NLP project: automated news article classification, benchmarking classical ML against a fine-tuned LLM — and the higher-F1 model isn't the one I picked. Here's why.
>
> **The problem**
> A news aggregation startup needs to categorize incoming articles into World / Sports / Business / Sci-Tech in real time. Manual triage doesn't scale.
>
> **What I built**
> Two pipelines on 4,000 articles (AG News, balanced):
>
> 1. Sentence Transformer (all-MiniLM-L6-v2) embeddings → Random Forest, with grid-search hyperparameter tuning
> 2. FLAN-T5-Large as a zero-shot classifier with two prompts — base vs. improved (added explicit category definitions)
>
> **Results (validation F1, weighted):**
> • Random Forest (tuned): **0.900**
> • FLAN-T5 base prompt: 0.935
> • FLAN-T5 improved prompt: 0.935
>
> **The decision**
> I chose the tuned Random Forest as the production model — despite FLAN-T5 scoring 3.5% higher on F1. Here's the math:
>
> ✅ RF predicts in milliseconds on CPU. FLAN-T5-Large takes seconds per article on GPU.
> ✅ RF runs on any server. FLAN-T5 needs a recurring GPU instance.
> ✅ At thousands of articles per day, the throughput and infra gap dwarfs the 3.5% F1.
>
> Final architecture: RF as primary, FLAN-T5 as a fallback for low-confidence predictions. Cheap on easy cases, smart on hard ones.
>
> **One thing I want to highlight**
> Same FLAN-T5 model, same temperature, same compute — just adding a one-line definition per category to the prompt nudged the confusion matrix in the right direction. Prompt engineering isn't a vibe, it's a measurable lever.
>
> Stack: Python · scikit-learn · sentence-transformers · Hugging Face · FLAN-T5 · PyTorch
>
> Full code + writeup → github.com/thehotpath/news-topic-classification
>
> #MachineLearning #NLP #DataScience #LLM #PromptEngineering

---

### 🖼️ Which graphs to attach to the post

LinkedIn lets you attach up to ~9 images. Pick **3–4** for max impact — don't dump everything:

1. **`images/00_model_comparison.png`** — the headline chart. This is the single image that tells the whole story. **Lead with this one.**
2. **`images/07_rf_tuned_valid_confusion.png`** — your final model's confusion matrix. Shows it actually works.
3. **`images/11_flan_improved_valid_confusion.png`** — the LLM result, with category definitions added to the prompt. Shows you compared approaches.
4. *(Optional)* **`images/01_class_distribution.png`** — clean EDA shot. Only include if you have the slot and want to look thorough.

Order matters: LinkedIn previews the first image. Lead with `00_model_comparison.png`.

---

## 🐙 Getting this on GitHub (step by step)

### Option A — via the web (easiest, no command line)

1. Go to **https://github.com/new**
2. Repository name: `news-topic-classification`
3. Description: `News article classification comparing Sentence Transformer + Random Forest vs. FLAN-T5 with prompt engineering`
4. Visibility: **Public**
5. Check ✅ "Add a README file" (you'll replace it)
6. Click **Create repository**
7. On the new repo page, click **Add file → Upload files**
8. Drag the entire contents of the downloaded repo folder into the upload area (README.md, requirements.txt, the `images/` folder, the `notebook/` folder)
9. Commit message: `Initial commit: NLP news classification project`
10. Click **Commit changes**

Your shareable link will be: **`https://github.com/thehotpath/news-topic-classification`**

### Option B — via git command line

```bash
# 1. Create the repo on github.com first (same as steps 1-6 above, but uncheck "Add a README")

# 2. Then on your local machine:
cd ~/Downloads/news-topic-classification     # or wherever you unzipped it
git init
git add .
git commit -m "Initial commit: NLP news classification project"
git branch -M main
git remote add origin https://github.com/thehotpath/news-topic-classification.git
git push -u origin main
```

---

## ✅ Final checklist before posting

- [ ] GitHub repo is **public** (otherwise the link 404s for recruiters)
- [ ] README renders correctly on the GitHub page (check the model comparison image loads)
- [ ] Notebook opens in GitHub preview (click the `.ipynb` file in the repo to confirm)
- [ ] LinkedIn post link points to your actual repo URL
- [ ] Attach 3–4 images in the order recommended above
- [ ] Pin this post to your profile so recruiters see it first
