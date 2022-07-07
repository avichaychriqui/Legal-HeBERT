# Legal-HeBERT
Legal-HeBERT is a BERT model for Hebrew legal and legislative domains. It is intended to improve the legal NLP research and tools development in Hebrew. We release two versions of Legal-HeBERT. The first version is a fine-tuned model of [HeBERT](https://github.com/avichaychriqui/HeBERT) applied on legal and legislative documents. The second version uses [HeBERT](https://github.com/avichaychriqui/HeBERT)'s architecture guidlines to train a BERT model from scratch. <br>
We continue collecting legal data, examining different architectural designs, and performing tagged datasets and legal tasks for evaluating and to development of a Hebrew legal tools.

## Training Data
Our training datasets are:
| Name | Hebrew Description | Size (GB) | Documents | Sentences | Words | Notes |
|---|---|---|---|---|---|---|
| The Israeli Law Book | ספר החוקים הישראלי | 0.05 | 2338 | 293352 | 4851063 |  |
| Judgments of the Supreme Court | מאגר פסקי   הדין של בית המשפט העליון | 0.7 | 212348 | 5790138 | 79672415 |  |
| custody courts | החלטות בתי   הדין למשמורת | 2.46 | 169,708 | 8,555,893 | 213,050,492 |  |
| Law memoranda, drafts of secondary legislation and drafts of   support tests that have been distributed to the public for comment | תזכירי חוק,   טיוטות חקיקת משנה וטיוטות מבחני תמיכה שהופצו להערות הציבור | 0.4 | 3,291 | 294,752 | 7,218,960 |  |
| Supervisors of Land Registration judgments | מאגר פסקי   דין של המפקחים על רישום המקרקעין | 0.02 | 559 | 67,639 | 1,785,446 |  |
| Decisions of the Labor Court - Corona |          מאגר החלטות   בית הדין לעניין שירות התעסוקה – קורונה | 0.001 | 146 | 3505 | 60195 |  |
| Decisions of the Israel Lands Council | החלטות   מועצת מקרקעי ישראל |   | 118 | 11283 | 162692 | aggregate file |
| Judgments of the Disciplinary Tribunal and the Israel Police Appeals Tribunal | פסקי  דין של בית הדין למשמעת ובית הדין לערעורים של משטרת ישראל | 0.02 | 54 | 83724 | 1743419 | aggregate files  |
| Disciplinary Appeals Committee in the   Ministry of Health | ועדת   ערר לדין משמעתי במשרד הבריאות | 0.004 | 252 | 21010 | 429807 | 465 files are scanned and didn't parser |
| Attorney General's Positions | מאגר התייצבויות היועץ המשפטי לממשלה | 0.008 | 281 | 32724 | 813877 |  |
| Legal-Opinion of the Attorney General | מאגר חוות דעת היועץ המשפטי לממשלה  | 0.002 | 44 | 7132 | 188053 |  |
|  |  |  |  |  |  |  |
| total |  | 3.665 | 389,139 | 15,161,152 | 309,976,419 |  |

We thank <b>Yair Gardin</b> for the referring to the governance data, <b>Elhanan Schwarts</b> for collecting and parsing The Israeli law book, and <b>Jonathan Schler</b> for collecting the judgments of the supreme court.


## Training process
* Vocabulary size: 50,000 tokens
* 4 epochs (1M steps±)
* lr=5e-5
* mlm_probability=0.15
* batch size = 32 (for each gpu)
* NVIDIA GeForce RTX 2080 TI + NVIDIA GeForce RTX 3090 (1 week training)

### Additional training settings: 
<b>Fine-tuned [HeBERT](https://github.com/avichaychriqui/HeBERT) model:</b> The first eight layers were freezed (like [Lee et al. (2019)](https://arxiv.org/abs/1911.03090) suggest)<br>
<b>Legal-HeBERT trained from scratch:</b> The training process is similar to [HeBERT](https://github.com/avichaychriqui/HeBERT) and inspired by [Chalkidis et al. (2020)](https://arxiv.org/abs/2010.02559) <br>

## How to use
The models can be found in huggingface hub and can be fine-tunned to any down-stream task:
```
# !pip install transformers==4.14.1
from transformers import AutoTokenizer, AutoModel

model_name = 'avichr/Legal-heBERT_ft' # for the fine-tuned HeBERT model 
model_name = 'avichr/Legal-heBERT' # for legal HeBERT model trained from scratch

tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModel.from_pretrained(model_name)

from transformers import pipeline
fill_mask = pipeline(
    "fill-mask",
    model=model_name,
)
fill_mask("הקורונה לקחה את [MASK] ולנו לא נשאר דבר.")
```
## Stay tuned!
We are still working on our models and the datasets. We will edit this page as we progress. We are open for collaborations.

## If you used this model please cite us as :
Chriqui, Avihay, Yahav, Inbal and Bar-Siman-Tov, Ittai, Legal HeBERT: A BERT-based NLP Model for Hebrew Legal, Judicial and Legislative Texts (June 27, 2022). Available at: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4147127

```
@article{chriqui2021hebert,
  title={Legal HeBERT: A BERT-based NLP Model for Hebrew Legal, Judicial and Legislative Texts},
  author={Chriqui, Avihay, Yahav, Inbal and Bar-Siman-Tov, Ittai},
  journal={SSRN preprint:4147127},
  year={2022}
}
```


## Contact us
[Avichay Chriqui](mailto:avichayc@mail.tau.ac.il), The Coller AI Lab <br>
[Inbal yahav](mailto:inbalyahav@tauex.tau.ac.il), The Coller AI Lab <br>
[Ittai Bar-Siman-Tov](mailto:Ittai.Bar-Siman-Tov@biu.ac.il), the BIU Innovation Lab for Law, Data-Science and Digital Ethics <br>

Thank you, תודה, شكرا <br>
