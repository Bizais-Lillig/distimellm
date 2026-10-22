**Task 1 : extract events**


3. V3 :

SYSTEM_PROMPT = """
CONTEXT: You are an annotator in a NLP research lab. Your job is to extract and annotate events in texts. 

ADDITIONAL CONTEXT:
The texts that you work on are in Modern Chinese, Ancient Chinese and English.
You extract only the events that have a temporal marker : a date, an expression (such as "last week", "after the meeting", "in the spring")
You pay attention to non-standard time expressions in classic Chinese (such as 鸡鸣, 东风解冻 or 一炷香).
Time may be given in either ISO format (YYYY-mm-dd) or in dynasty, era, reign, sexagenary, month and/or season, double hour format. 
Dates are not to be converted, slots are filled in the original format expressed in the text. 


MANDATORY RESPONSE FORMAT: A JSON structured text. 
Expected JSON structure:
"events":
    [
        {"event_id": "prefix+integer",
        "event_text": "exact string in the text where the event is mentioned", 
        "event_sources":
        [{"filename": "str",
        "time_related_expr":["str"],
        "position_in_text":["int : first character"]}        
        ],
        "time_start": "OPTIONAL tuple(min_start_time, max_start_time) OR Null)",
        "time_end": "OPTIONAL tuple(min_end_time, max_end_time) OR Null)",
        "range": "OPTIONAL tuple of tuples: (min(unit,value), max(unit,value)) OR Null"
    }

INSTRUCTIONS :
- DO NOT INVENT time if not explicitely given in the text
- **DO NOT INFER** time information to fill all slots
- DO NOT CONVERT into ISO format if date is not given in ISO format.
- CREATE "event_id", a unique identifier for each event, using the filename
- DO NOT CREATE ANY OTHER INFORMATION than event_id
"""

```json
{
  "events": [
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_00",
      "event_text": "燬焉",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["至元丙子"],
          "position_in_text": [50]
        }
      ],
      "time_start": ["至元丙子", "至元丙子"],
      "time_end": ["至元丙子", "至元丙子"],
      "range": null
    },
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_01",
      "event_text": "民病渉為梁以濟",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["壬辰六月"],
          "position_in_text": [63]
        }
      ],
      "time_start": ["壬辰六月", "壬辰六月"],
      "time_end": ["壬辰六月", "壬辰六月"],
      "range": null
    },
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_02",
      "event_text": "始事",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["癸已十一月"],
          "position_in_text": [96]
        }
      ],
      "time_start": ["癸已十一月", "癸已十一月"],
      "time_end": ["癸已十一月", "癸已十一月"],
      "range": null
    },
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_03",
      "event_text": "落成",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["越明年七月"],
          "position_in_text": [106]
        }
      ],
      "time_start": ["越明年七月", "越明年七月"],
      "time_end": ["越明年七月", "越明年七月"],
      "range": null
    },
    {
      "event_id": "po_en_1669_00",
      "event_text": "President Chen Shui-bian presided over a ceremony Wednesday in Puli township, central Nantou County to kick off construction of the Nantou section of the National Expressway No. 6.",
      "event_sources": [
        {
          "filename": "po_en_1669.txt",
          "time_related_expr": ["Feb. 25", "Wednesday"],
          "position_in_text": [8, 72]
        }
      ],
      "time_start": ["XXXX-02-25", "XXXX-02-25"],
      "time_end": ["XXXX-02-25", "XXXX-02-25"],
      "range": null
    },
    {
      "event_id": "SPSP192606271118_00",
      "event_text": "以清華官學生出洋入美國俄伯靈大學經濟銀行科",
      "event_sources": [
        {
          "filename": "SPSP192606271118.txt",
          "time_related_expr": ["民國十三年八月"],
          "position_in_text": [72]
        }
      ],
      "time_start": ["民國十三年八月", "民國十三年八月"],
      "time_end": ["民國十三年八月", "民國十三年八月"],
      "range": null
    },
    {
      "event_id": "SPSP192606271118_01",
      "event_text": "以第一名畢業獲學士位",
      "event_sources": [
        {
          "filename": "SPSP192606271118.txt",
          "time_related_expr": ["十五年二月"],
          "position_in_text": [110]
        }
      ],
      "time_start": ["十五年二月", "十五年二月"],
      "time_end": ["十五年二月", "十五年二月"],
      "range": null
    },
    {
      "event_id": "SPSP192506121501_00",
      "event_text": "上海扶輪社日前接天津扶輪社來電",
      "event_sources": [
        {
          "filename": "SPSP192506121501.txt",
          "time_related_expr": ["日前"],
          "position_in_text": [9]
        }
      ],
      "time_start": ["日前", "日前"],
      "time_end": ["日前", "日前"],
      "range": null
    },
    {
      "event_id": "1319854677_00",
      "event_text": "Proclamations were issued this week enjoining the slaughter of pigs oxen sheep and goats for three days",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["this week"],
          "position_in_text": [130]
        }
      ],
      "time_start": ["this week", "this week"],
      "time_end": ["this week", "this week"],
      "range": null
    },
    {
      "event_id": "1319854677_01",
      "event_text": "Bitter opposition has been raised this week among all classes of people in Peking against the newly proposed police tax",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["this week"],
          "position_in_text": [565]
        }
      ],
      "time_start": ["this week", "this week"],
      "time_end": ["this week", "this week"],
      "range": null
    },
    {
      "event_id": "1319854677_02",
      "event_text": "Liang Tun-yen well-known Chinese scholar of the old type and one of the earliest American returned students passed away at his Peking residence",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["on May 12"],
          "position_in_text": [1330]
        }
      ],
      "time_start": ["XXXX-05-12", "XXXX-05-12"],
      "time_end": ["XXXX-05-12", "XXXX-05-12"],
      "range": null
    },
    {
      "event_id": "1319854677_03",
      "event_text": "General Li Yuan-hung former president of China has returned to his Tientsin resilience from long visit in Japan",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["on May 10"],
          "position_in_text": [1600]
        }
      ],
      "time_start": ["XXXX-05-10", "XXXX-05-10"],
      "time_end": ["XXXX-05-10", "XXXX-05-10"],
      "range": null
    },
    {
      "event_id": "1319854677_04",
      "event_text": "By presidential mandates issued Monday night Yueh Chao-chu councillor of the ministry of foreign affairs was appointed minister to Mexico and Chang Chien Jr was appointed minister to Chile",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["Monday night"],
          "position_in_text": [1750]
        }
      ],
      "time_start": ["Monday night", "Monday night"],
      "time_end": ["Monday night", "Monday night"],
      "range": null
    },
    {
      "event_id": "1319854677_05",
      "event_text": "two of the main lines of the Peking tramways will be operation",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["on July 1"],
          "position_in_text": [2400]
        }
      ],
      "time_start": ["XXXX-07-01", "XXXX-07-01"],
      "time_end": ["XXXX-07-01", "XXXX-07-01"],
      "range": null
    },
    {
      "event_id": "1319854677_06",
      "event_text": "about 200 in number who held meeting in the Central Park of Peking",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 15"],
          "position_in_text": [2900]
        }
      ],
      "time_start": ["XXXX-05-15", "XXXX-05-15"],
      "time_end": ["XXXX-05-15", "XXXX-05-15"],
      "range": null
    },
    {
      "event_id": "1319854677_07",
      "event_text": "Burgess secretary of the Community Service depart ment of the Peking left for Shanghai",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 15"],
          "position_in_text": [3500]
        }
      ],
      "time_start": ["XXXX-05-15", "XXXX-05-15"],
      "time_end": ["XXXX-05-15", "XXXX-05-15"],
      "range": null
    },
    {
      "event_id": "1319854677_08",
      "event_text": "Dr Jacob Gould Schurman the American Minister to China accompanied by Mrs Schurman left Peking",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 14"],
          "position_in_text": [3800]
        }
      ],
      "time_start": ["XXXX-05-14", "XXXX-05-14"],
      "time_end": ["XXXX-05-14", "XXXX-05-14"],
      "range": null
    },
    {
      "event_id": "1319854677_09",
      "event_text": "General William Conner commander of the 15th Infantry at Tientsin accompanied by his aides and Mr Peck Chinese secretary of the American Legation left Peking",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 12"],
          "position_in_text": [4400]
        }
      ],
      "time_start": ["XXXX-05-12", "XXXX-05-12"],
      "time_end": ["XXXX-05-12", "XXXX-05-12"],
      "range": null
    },
    {
      "event_id": "1319854677_10",
      "event_text": "Hiram Cleaver ex-president of the Continental Oil Company of Denver Colorado and Mrs Cleaver arrived in Peking",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 14"],
          "position_in_text": [4700]
        }
      ],
      "time_start": ["XXXX-05-14", "XXXX-05-14"],
      "time_end": ["XXXX-05-14", "XXXX-05-14"],
      "range": null
    },
    {
      "event_id": "KR4d0232-WYG-f006-0002_撫州新作浮橋記_00",
      "event_text": "始作浮梁以通徃來",
      "event_sources": [
        {
          "filename": "KR4d0232-WYG-f006-0002_撫州新作浮橋記.txt",
          "time_related_expr": ["乾道初元"],
          "position_in_text": [15]
        }
      ],
      "time_start": ["乾道初元", "乾道初元"],
      "time_end": ["乾道初元", "乾道初元"],
      "range": null
    },
    {
      "event_id": "KR4d0232-WYG-f006-0002_撫州新作浮橋記_01",
      "event_text": "甚雨淫潦漂航斷笮無一存者",
      "event_sources": [
        {
          "filename": "KR4d0232-WYG-f006-0002_撫州新作浮橋記.txt",
          "time_related_expr": ["淳熈二年秋七月"],
          "position_in_text": [30]
        }
      ],
      "time_start": ["淳熈二年秋七月", "淳熈二年秋七月"],
      "time_end": ["淳熈二年秋七月", "淳熈二年秋七月"],
      "range": null
    },
    {
      "event_id": "KR4d0232-WYG-f006-0002_撫州新作浮橋記_02",
      "event_text": "造端",
      "event_sources": [
        {
          "filename": "KR4d0232-WYG-f006-0002_撫州新作浮橋記.txt",
          "time_related_expr": ["十月戊寅"],
          "position_in_text": [90]
        }
      ],
      "time_start": ["十月戊寅", "十月戊寅"],
      "time_end": ["十月戊寅", "十月戊寅"],
      "range": null
    },
    {
      "event_id": "KR4d0232-WYG-f006-0002_撫州新作浮橋記_03",
      "event_text": "告具",
      "event_sources": [
        {
          "filename": "KR4d0232-WYG-f006-0002_撫州新作浮橋記.txt",
          "time_related_expr": ["十一月丁丑"],
          "position_in_text": [100]
        }
      ],
      "time_start": ["十一月丁丑", "十一月丁丑"],
      "time_end": ["十一月丁丑", "十一月丁丑"],
      "range": null
    },
    {
      "event_id": "1319843498_00",
      "event_text": "at the in Shanghai 120 women enrolled for ten days course of lectures on these subjects",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["last week"],
          "position_in_text": [250]
        }
      ],
      "time_start": ["last week", "last week"],
      "time_end": ["last week", "last week"],
      "range": null
    },
    {
      "event_id": "1319843498_01",
      "event_text": "Jean Alvalyn was born to Mr and Mrs Cannon at Foochow China",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on November 6"],
          "position_in_text": [2500]
        }
      ],
      "time_start": ["XXXX-11-06", "XXXX-11-06"],
      "time_end": ["XXXX-11-06", "XXXX-11-06"],
      "range": null
    },
    {
      "event_id": "1319843498_02",
      "event_text": "social evening hearts drive and dance will be held in the Municipal Service Club No 8-b Peking Road to members and their friends only",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Friday November 14"],
          "position_in_text": [2600]
        }
      ],
      "time_start": ["XXXX-11-14", "XXXX-11-14"],
      "time_end": ["XXXX-11-14", "XXXX-11-14"],
      "range": null
    },
    {
      "event_id": "1319843498_03",
      "event_text": "Mrs George Fryer will be at home to her freinds at No 4 Edinburgh Road Shanghai",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["during the second and third Fridays November 14 and 21 from 4 to 6"],
          "position_in_text": [2700]
        }
      ],
      "time_start": ["XXXX-11-14", "XXXX-11-14"],
      "time_end": ["XXXX-11-21", "XXXX-11-21"],
      "range": null
    },
    {
      "event_id": "1319843498_04",
      "event_text": "The announcement is made of the marriage of Dr Amy Metcalf formerly of the American Board Mission for four years in North China and Capt Albert Bowen at Tours France",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on October 29"],
          "position_in_text": [2900]
        }
      ],
      "time_start": ["XXXX-10-29", "XXXX-10-29"],
      "time_end": ["XXXX-10-29", "XXXX-10-29"],
      "range": null
    },
    {
      "event_id": "1319843498_05",
      "event_text": "reception was given to parents and their friends by the faculty",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Tuesday afternoon Novem ber xi"],
          "position_in_text": [3200]
        }
      ],
      "time_start": ["XXXX-11-11", "XXXX-11-11"],
      "time_end": ["XXXX-11-11", "XXXX-11-11"],
      "range": null
    },
    {
      "event_id": "1319843498_06",
      "event_text": "The wedding took place at Hankow China",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on No vember 2"],
          "position_in_text": [3500]
        }
      ],
      "time_start": ["XXXX-11-02", "XXXX-11-02"],
      "time_end": ["XXXX-11-02", "XXXX-11-02"],
      "range": null
    },
    {
      "event_id": "1319843498_07",
      "event_text": "More than 400 members of the Shanghai com munity and their guests were present at the Armistice celebration at the Shanghai Club",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Tuesday evening November 11"],
          "position_in_text": [3800]
        }
      ],
      "time_start": ["XXXX-11-11", "XXXX-11-11"],
      "time_end": ["XXXX-11-11", "XXXX-11-11"],
      "range": null
    },
    {
      "event_id": "1319843498_08",
      "event_text": "plan to hold an informal dinner during the winter season to entertain the officers and men of the American warships in harbor at the Navy at No 6 Avenue Edward VII under the auspices of the American Woman's Club and the Navy was decided at their first at home",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Saturday evening November 8"],
          "position_in_text": [4200]
        }
      ],
      "time_start": ["XXXX-11-08", "XXXX-11-08"],
      "time_end": ["XXXX-11-08", "XXXX-11-08"],
      "range": null
    },
    {
      "event_id": "1319843498_09",
      "event_text": "At dinner given by YangTcheng Commissioner of Foreign Affairs at the Naval Club",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Saturday evening November 8"],
          "position_in_text": [4500]
        }
      ],
      "time_start": ["XXXX-11-08", "XXXX-11-08"],
      "time_end": ["XXXX-11-08", "XXXX-11-08"],
      "range": null
    },
    {
      "event_id": "po_zh_8342_00",
      "event_text": "前往南投縣埔里鎮參加國道六號南投段開工動土典禮，並應邀致詞",
      "event_sources": [
        {
          "filename": "po_zh_8342.txt",
          "time_related_expr": ["今天下午"],
          "position_in_text": [10]
        }
      ],
      "time_start": ["今天下午", "今天下午"],
      "time_end": ["今天下午", "今天下午"],
      "range": null
    },
    {
      "event_id": "po_zh_8342_01",
      "event_text": "「中二高」南投路段完工通車",
      "event_sources": [
        {
          "filename": "po_zh_8342.txt",
          "time_related_expr": ["兩年前"],
          "position_in_text": [300]
        }
      ],
      "time_start": ["兩年前", "兩年前"],
      "time_end": ["兩年前", "兩年前"],
      "range": null
    },
    {
      "event_id": "po_zh_8342_02",
      "event_text": "「第二高速公路」於今年1月全線通車",
      "event_sources": [
        {
          "filename": "po_zh_8342.txt",
          "time_related_expr": ["今年1月"],
          "position_in_text": [700]
        }
      ],
      "time_start": ["今年1月", "今年1月"],
      "time_end": ["今年1月", "今年1月"],
      "range": null
    },
    {
      "event_id": "po_zh_8342_03",
      "event_text": "「高速鐵路」於明年十月開始營運通車",
      "event_sources": [
        {
          "filename": "po_zh_8342.txt",
          "time_related_expr": ["明年十月"],
          "position_in_text": [750]
        }
      ],
      "time_start": ["明年十月", "明年十月"],
      "time_end": ["明年十月", "明年十月"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_00",
      "event_text": "考入清華官費出洋抵美",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二一年"],
          "position_in_text": [50]
        }
      ],
      "time_start": ["一九二一年", "一九二一年"],
      "time_end": ["一九二一年", "一九二一年"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_01",
      "event_text": "受碩士銜",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二五年"],
          "position_in_text": [150]
        }
      ],
      "time_start": ["一九二五年", "一九二五年"],
      "time_end": ["一九二五年", "一九二五年"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_02",
      "event_text": "取道歐洲藉以考查各國敎育狀况後始行回國",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["今夏七月間"],
          "position_in_text": [250]
        }
      ],
      "time_start": ["今夏七月間", "今夏七月間"],
      "time_end": ["今夏七月間", "今夏七月間"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_03",
      "event_text": "赴美留學",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二一年"],
          "position_in_text": [400]
        }
      ],
      "time_start": ["一九二一年", "一九二一年"],
      "time_end": ["一九二一年", "一九二一年"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_04",
      "event_text": "回國",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二六年春季"],
          "position_in_text": [450]
        }
      ],
      "time_start": ["一九二六年春季", "一九二六年春季"],
      "time_end": ["一九二六年春季", "一九二六年春季"],
      "range": null
    },
    {
      "event_id": "SPSP193109022001_00",
      "event_text": "上海扶輪社本星期四午間十二時三十分、在老卡爾登舉行聚餐會、請安德魯博士演講最近探險蒙古沙漠情形",
      "event_sources": [
        {
          "filename": "SPSP193109022001.txt",
          "time_related_expr": ["本星期四午間十二時三十分"],
          "position_in_text": [10]
        }
      ],
      "time_start": ["本星期四午間十二時三十分", "本星期四午間十二時三十分"],
      "time_end": ["本星期四午間十二時三十分", "本星期四午間十二時三十分"],
      "range": null
    }
  ]
}
```

2. V2 :

SYSTEM_PROMPT = """
CONTEXT: You are an annotator in a NLP research lab. Your job is to extract and annotate events in texts. 

ADDITIONAL CONTEXT:
The texts that you work on are in Modern Chinese, Ancient Chinese and English.
You extract only the events that have a temporal marker : a date, an expression (such as "last week", "after the meeting", "in the spring")
You pay attention to non-standard time expressions in classic Chinese (such as 鸡鸣, 东风解冻 or 一炷香).
Time may be given in either ISO format (YYYY-mm-dd) or in dynasty, era, reign, sexagenary, month and/or season, double hour format. 
Dates are not to be converted, slots are filled in the original format expressed in the text. 


MANDATORY RESPONSE FORMAT: A JSON structured text. 
Expected JSON structure:
"events":
    [
        {"event_id": "prefix+integer",
        "event_text": "exact string in the text where the event is mentioned", 
        "event_sources":
        [{"filename": "str",
        "time_related_expr":["str"],
        "position_in_text":["int : first character"]}        
        ],
        "time_start": "tuple(min_start_timestamp, max_start_timestamp) OR Null)",
        "time_end": "tuple(min_end_timestamp, max_end_timestamp) OR Null)",
        "range": "tuple of tuples: (min(unit,value), max(unit,value)) OR Null"
    }

INSTRUCTIONS :
- DO NOT INVENT time if not explicitely given in the text
- **DO NOT INFER** time information to fill all slots
- DO NOT CONVERT into ISO format if date is not given in ISO format.
- CREATE "event_id", a unique identifier for each event, using the filename
- DO NOT CREATE ANY OTHER INFORMATION than event_id
"""


#We should provide a calendar conversion

```json
{
  "events": [
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_00",
      "event_text": "壬辰六月郡侯章公總管趙公帥同僚洎郡寓公大家度材鳩工",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["壬辰六月"],
          "position_in_text": [77]
        }
      ],
      "time_start": ["(1292-06-01)", "(1292-06-30)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_01",
      "event_text": "癸已十一月始事",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["癸已十一月"],
          "position_in_text": [101]
        }
      ],
      "time_start": ["(1293-11-01)", "(1293-11-30)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_02",
      "event_text": "越明年七月落成",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["越明年七月"],
          "position_in_text": [111]
        }
      ],
      "time_start": ["(1294-07-01)", "(1294-07-30)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_03",
      "event_text": "由丙子至甲午幾二十年而橋始復太平之世民有餘力",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["由丙子至甲午幾二十年"],
          "position_in_text": [208]
        }
      ],
      "time_start": ["(1276-01-01)", "(1276-12-31)"],
      "time_end": ["(1294-01-01)", "(1294-12-31)"],
      "range": [["year", 18], ["year", 19]]
    },
    {
      "event_id": "po_en_1669_00",
      "event_text": "President Chen Shui-bian presided over a ceremony Wednesday in Puli township, central Nantou County to kick off construction of the Nantou section of the National Expressway No. 6.",
      "event_sources": [
        {
          "filename": "po_en_1669.txt",
          "time_related_expr": ["Wednesday"],
          "position_in_text": [8]
        }
      ],
      "time_start": ["(2004-02-25)", "(2004-02-25)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "SPSP192606271118_00",
      "event_text": "民國十三年八月以清華官學生出洋入美國俄伯靈大學經濟銀行科",
      "event_sources": [
        {
          "filename": "SPSP192606271118.txt",
          "time_related_expr": ["民國十三年八月"],
          "position_in_text": [78]
        }
      ],
      "time_start": ["(1924-08-01)", "(1924-08-31)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "SPSP192606271118_01",
      "event_text": "十五年二月以第一名畢業獲學士位",
      "event_sources": [
        {
          "filename": "SPSP192606271118.txt",
          "time_related_expr": ["十五年二月"],
          "position_in_text": [112]
        }
      ],
      "time_start": ["(1926-02-01)", "(1926-02-28)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "SPSP192506121501_00",
      "event_text": "天津扶輪社電上海扶輪社日前接天津扶輪社來電",
      "event_sources": [
        {
          "filename": "SPSP192506121501.txt",
          "time_related_expr": ["日前"],
          "position_in_text": [11]
        }
      ],
      "time_start": ["(1925-06-01)", "(1925-06-11)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_00",
      "event_text": "Proclamations were issued this week enjoining the slaughter of pigs oxen sheep and goats for three days",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["this week"],
          "position_in_text": [106]
        }
      ],
      "time_start": ["(1924-05-12)", "(1924-05-17)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_01",
      "event_text": "Bitter opposition has been raised this week among all classes of people in Peking against the newly proposed police tax",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["this week"],
          "position_in_text": [480]
        }
      ],
      "time_start": ["(1924-05-12)", "(1924-05-17)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_02",
      "event_text": "Liang Tun-yen well-known Chinese scholar of the old type and one of the earliest American returned students passed away at his Peking residence on May 12.",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["on May 12"],
          "position_in_text": [1091]
        }
      ],
      "time_start": ["(1924-05-12)", "(1924-05-12)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_03",
      "event_text": "General Li Yuan-hung former president of China has returned to his Tientsin resilience from long visit in Japan on May 10.",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["on May 10"],
          "position_in_text": [1420]
        }
      ],
      "time_start": ["(1924-05-10)", "(1924-05-10)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_04",
      "event_text": "By presidential mandates issued Monday night Yueh Chao-chu councillor of the ministry of foreign affairs was appointed minister to Mexico and Chang Chien Jr was appointed minister to Chile",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["Monday night"],
          "position_in_text": [1580]
        }
      ],
      "time_start": ["(1924-05-12)", "(1924-05-12)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_05",
      "event_text": "The news lias been given out by the Peking Tramway company that two of the main lines of the Peking tramways will be operation on July 1.",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["on July 1"],
          "position_in_text": [2410]
        }
      ],
      "time_start": ["(1924-07-01)", "(1924-07-01)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_06",
      "event_text": "number of Chinese P's about 200 in number who held meeting in the Central Park of Peking May 15, and passed resolution that tlie government should request the British Legation to close up the British Legation Guards' Club in Mei Cha Hutung",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 15"],
          "position_in_text": [2960]
        }
      ],
      "time_start": ["(1924-05-15)", "(1924-05-15)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_07",
      "event_text": "Burgess secretary of the Community Service depart ment of the Peking left for Shanghai May 15, to be away for about three weeks",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 15"],
          "position_in_text": [3860]
        }
      ],
      "time_start": ["(1924-05-15)", "(1924-05-15)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_08",
      "event_text": "Dr Jacob Gould Schurman the American Minister to China accompanied by Mrs Schurman left Peking May 14, for Tientsin where Dr Schurman spoke before the Tientsin Rotary Club and also to the students of the Nankai university",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 14"],
          "position_in_text": [4100]
        }
      ],
      "time_start": ["(1924-05-14)", "(1924-05-14)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_09",
      "event_text": "General William Conner commander of the 15th Infantry at Tientsin accompanied by his aides and Mr Peck Chinese secretary of the American Legation left Peking May 12, for Loyang where they will be guests of General Wu Pei-fu for few days",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 12"],
          "position_in_text": [4650]
        }
      ],
      "time_start": ["(1924-05-12)", "(1924-05-12)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_10",
      "event_text": "Hiram Cleaver ex-president of the Continental Oil Company of Denver Colorado and Mrs Cleaver arrived in Peking May 14.",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 14"],
          "position_in_text": [4870]
        }
      ],
      "time_start": ["(1924-05-14)", "(1924-05-14)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "KR4d0232-WYG-f006-0002_撫州新作浮橋記_00",
      "event_text": "淳熈二年秋七月甚雨淫潦漂航斷笮無一存者",
      "event_sources": [
        {
          "filename": "KR4d0232-WYG-f006-0002_撫州新作浮橋記.txt",
          "time_related_expr": ["淳熈二年秋七月"],
          "position_in_text": [38]
        }
      ],
      "time_start": ["(1175-07-01)", "(1175-07-31)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "KR4d0232-WYG-f006-0002_撫州新作浮橋記_01",
      "event_text": "造端以十月戊寅",
      "event_sources": [
        {
          "filename": "KR4d0232-WYG-f006-0002_撫州新作浮橋記.txt",
          "time_related_expr": ["十月戊寅"],
          "position_in_text": [109]
        }
      ],
      "time_start": ["(1175-10-01)", "(1175-10-30)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "KR4d0232-WYG-f006-0002_撫州新作浮橋記_02",
      "event_text": "告具以十一月丁丑",
      "event_sources": [
        {
          "filename": "KR4d0232-WYG-f006-0002_撫州新作浮橋記.txt",
          "time_related_expr": ["十一月丁丑"],
          "position_in_text": [116]
        }
      ],
      "time_start": ["(1175-11-01)", "(1175-11-30)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_00",
      "event_text": "yet last week at the in Shanghai 120 women enrolled for ten days course of lectures on these subjects coming daily from 3 to 5: 30.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["last week"],
          "position_in_text": [220]
        }
      ],
      "time_start": ["(1917-10-29)", "(1917-11-04)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_01",
      "event_text": "Jean Alvalyn was born to Mr and Mrs Cannon at Foochow China on November 6.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on November 6"],
          "position_in_text": [2370]
        }
      ],
      "time_start": ["(1917-11-06)", "(1917-11-06)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_02",
      "event_text": "social evening hearts drive and dance will be held in the Municipal Service Club No 8-b Peking Road to members and their friends only on Friday November 14.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Friday November 14"],
          "position_in_text": [2450]
        }
      ],
      "time_start": ["(1917-11-14)", "(1917-11-14)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_03",
      "event_text": "Mrs George Fryer will be at home to her freinds at No 4 Edinburgh Road Shanghai during the second and third Fridays November 14 and 21 from 4 to 6",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["November 14 and 21"],
          "position_in_text": [2580]
        }
      ],
      "time_start": ["(1917-11-14)", "(1917-11-14)"],
      "time_end": ["(1917-11-21)", "(1917-11-21)"],
      "range": null
    },
    {
      "event_id": "1319843498_04",
      "event_text": "The announcement is made of the marriage of Dr Amy Metcalf formerly of the American Board Mission for four years in North China and Capt Albert Bowen at Tours France on October 29.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on October 29"],
          "position_in_text": [2780]
        }
      ],
      "time_start": ["(1917-10-29)", "(1917-10-29)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_05",
      "event_text": "Mrs Bowen left China in June for France",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["in June"],
          "position_in_text": [2940]
        }
      ],
      "time_start": ["(1917-06-01)", "(1917-06-30)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_06",
      "event_text": "At the home of the faculty of the Shanghai American School at No 147 Szechuen Road Shanghai reception was given to parents and their friends by the faculty on Tuesday afternoon Novem ber xi",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Tuesday afternoon Novem ber xi"],
          "position_in_text": [3080]
        }
      ],
      "time_start": ["(1917-11-11)", "(1917-11-11)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_07",
      "event_text": "The wedding took place at Hankow China on No vember 2, of John Bristow of the Standard Oil Com pany at Shanghai and Miss Frances Helen Blair at the home of Mr and Mrs Gale",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on No vember 2"],
          "position_in_text": [3460]
        }
      ],
      "time_start": ["(1917-11-02)", "(1917-11-02)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_08",
      "event_text": "More than 400 members of the Shanghai com munity and their guests were present at the Armistice celebration at the Shanghai Club on Tuesday evening November 11.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Tuesday evening November 11"],
          "position_in_text": [3800]
        }
      ],
      "time_start": ["(1917-11-11)", "(1917-11-11)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_09",
      "event_text": "plan to hold an informal dinner during the winter season to entertain the officers and men of the American warships in harbor at the Navy at No 6 Avenue Edward VII under the auspices of the American Woman's Club and the Navy was decided at their first at home held on Saturday evening November 8, at which more than 60 guests were present",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Saturday evening November 8"],
          "position_in_text": [4300]
        }
      ],
      "time_start": ["(1917-11-08)", "(1917-11-08)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_10",
      "event_text": "At dinner given by YangTcheng Commissioner of Foreign Affairs at the Naval Club on Saturday evening November 8, the following guests were present",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Saturday evening November 8"],
          "position_in_text": [4780]
        }
      ],
      "time_start": ["(1917-11-08)", "(1917-11-08)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "SPSP192708311019_00",
      "event_text": "一九二一年考入清華官費出洋抵美後攻讀敎育管理專科三年卒業於芝加哥大學",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二一年"],
          "position_in_text": [43]
        }
      ],
      "time_start": ["(1921-01-01)", "(1921-12-31)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "SPSP192708311019_01",
      "event_text": "一九二五年受碩士銜",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二五年"],
          "position_in_text": [137]
        }
      ],
      "time_start": ["(1925-01-01)", "(1925-12-31)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "SPSP192708311019_02",
      "event_text": "女士已於今夏七月間取道歐洲藉以考查各國敎育狀况後始行回國",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["今夏七月間"],
          "position_in_text": [220]
        }
      ],
      "time_start": ["(1927-07-01)", "(1927-07-31)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "SPSP192708311019_03",
      "event_text": "一九二一年赴美留學卒業於新英倫音樂專科學院",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二一年"],
          "position_in_text": [320]
        }
      ],
      "time_start": ["(1921-01-01)", "(1921-12-31)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "SPSP192708311019_04",
      "event_text": "一九二六年春季回國現執音樂敎鞭於中西女塾母校",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二六年春季"],
          "position_in_text": [350]
        }
      ],
      "time_start": ["(1926-03-01)", "(1926-05-31)"],
      "time_end": null,
      "range": null
    },
    {
      "event_id": "SPSP193109022001_00",
      "event_text": "上海扶輪社本星期四午間十二時三十分、在老卡爾登舉行聚餐會、請安德魯博士演講最近探險蒙古沙漠情形",
      "event_sources": [
        {
          "filename": "SPSP193109022001.txt",
          "time_related_expr": ["本星期四午間十二時三十分"],
          "position_in_text": [8]
        }
      ],
      "time_start": ["(1931-09-03)", "(1931-09-03)"],
      "time_end": null,
      "range": null
    }
  ]
}
```



1. V1 :

SYSTEM_PROMPT = """
CONTEXT: You are an annotator in a NLP research lab. Your job is to extract and annotate events in texts. 

ADDITIONAL CONTEXT:
The texts that you work on are in Modern Chinese, Ancient Chinese and English.
You extract only the events that have a temporal marker : a date, an expression (such as "last week", "after the meeting", "in the spring")
You pay attention to non-standard time expressions in classic Chinese (such as 鸡鸣, 东风解冻 or 一炷香).
Time may be given in either ISO format (YYYY-mm-dd) or in dynasty, era, reign, sexagenary, month and/or season, double hour format. 

MANDATORY RESPONSE FORMAT: A JSON structured text. 
Expected JSON structure:
"events":
    [
        {"event_id": "prefix+integer",
        "event_text": "exact string in the text where the event is mentioned", 
        "event_sources":
        [{"filename": "str",
        "time_related_expr":["str"],
        "position_in_text":["int : first character"]}        
        ],
        "time_start": "tuple(min_start_timestamp, max_start_timestamp) OR Null)",
        "time_end": "tuple(min_end_timestamp, max_end_timestamp) OR Null)",
        "range": "tuple of tuples: (min(unit,value), max(unit,value)) OR Null"
    }

INSTRUCTIONS :
- DO NOT INVENT time if not explicitely given in the text
- **DO NOT INFER** time information to fill all slots
- CREATE "event_id", a unique identifier for each event, using the filename
- DO NOT CREATE ANY OTHER INFORMATION than event_id
"""


#We should provide a calendar conversion


RESULTS :

```json
{
  "events": [
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_00",
      "event_text": "壬辰六月郡侯章公總管趙公帥同僚洎郡寓公大家度材鳩工",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["壬辰六月"],
          "position_in_text": [96]
        }
      ],
      "time_start": ["1292-06-01", "1292-06-30"],
      "time_end": ["1292-06-01", "1292-06-30"],
      "range": null
    },
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_01",
      "event_text": "癸已十一月始事",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["癸已十一月"],
          "position_in_text": [126]
        }
      ],
      "time_start": ["1293-11-01", "1293-11-30"],
      "time_end": ["1293-11-01", "1293-11-30"],
      "range": null
    },
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_02",
      "event_text": "越明年七月落成",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["越明年七月"],
          "position_in_text": [137]
        }
      ],
      "time_start": ["1294-07-01", "1294-07-30"],
      "time_end": ["1294-07-01", "1294-07-30"],
      "range": null
    },
    {
      "event_id": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記_03",
      "event_text": "由丙子至甲午幾二十年而橋始復太平之世民有餘力",
      "event_sources": [
        {
          "filename": "KR4d0466-WYG-f011-0010_建昌路重建太平橋記.txt",
          "time_related_expr": ["由丙子至甲午幾二十年"],
          "position_in_text": [283]
        }
      ],
      "time_start": ["1276-01-01", "1276-12-31"],
      "time_end": ["1294-01-01", "1294-12-31"],
      "range": [["year", 18], ["year", 20]]
    },
    {
      "event_id": "po_en_1669_00",
      "event_text": "President Chen Shui-bian presided over a ceremony Wednesday in Puli township, central Nantou County to kick off construction of the Nantou section of the National Expressway No. 6.",
      "event_sources": [
        {
          "filename": "po_en_1669.txt",
          "time_related_expr": ["Wednesday"],
          "position_in_text": [37]
        }
      ],
      "time_start": ["2004-02-25", "2004-02-25"],
      "time_end": ["2004-02-25", "2004-02-25"],
      "range": null
    },
    {
      "event_id": "SPSP192606271118_00",
      "event_text": "民國十三年八月以清華官學生出洋入美國俄伯靈大學經濟銀行科",
      "event_sources": [
        {
          "filename": "SPSP192606271118.txt",
          "time_related_expr": ["民國十三年八月"],
          "position_in_text": [87]
        }
      ],
      "time_start": ["1924-08-01", "1924-08-31"],
      "time_end": ["1924-08-01", "1924-08-31"],
      "range": null
    },
    {
      "event_id": "SPSP192606271118_01",
      "event_text": "十五年二月以第一名畢業獲學士位",
      "event_sources": [
        {
          "filename": "SPSP192606271118.txt",
          "time_related_expr": ["十五年二月"],
          "position_in_text": [130]
        }
      ],
      "time_start": ["1926-02-01", "1926-02-28"],
      "time_end": ["1926-02-01", "1926-02-28"],
      "range": null
    },
    {
      "event_id": "SPSP192506121501_00",
      "event_text": "天津扶輪社電上海扶輪社日前接天津扶輪社來電",
      "event_sources": [
        {
          "filename": "SPSP192506121501.txt",
          "time_related_expr": ["日前"],
          "position_in_text": [13]
        }
      ],
      "time_start": null,
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_00",
      "event_text": "Proclamations were issued this week enjoining the slaughter of pigs oxen sheep and goats for three days with severe penalty for failure to do so",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["this week"],
          "position_in_text": [107]
        }
      ],
      "time_start": null,
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_01",
      "event_text": "Liang Tun-yen well-known Chinese scholar of the old type and one of the earliest American returned students passed away at his Peking residence on May 12.",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["on May 12"],
          "position_in_text": [1504]
        }
      ],
      "time_start": ["1924-05-12", "1924-05-12"],
      "time_end": ["1924-05-12", "1924-05-12"],
      "range": null
    },
    {
      "event_id": "1319854677_02",
      "event_text": "General Li Yuan-hung former president of China has returned to his Tientsin resilience from long visit in Japan on May 10.",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["on May 10"],
          "position_in_text": [1918]
        }
      ],
      "time_start": ["1924-05-10", "1924-05-10"],
      "time_end": ["1924-05-10", "1924-05-10"],
      "range": null
    },
    {
      "event_id": "1319854677_03",
      "event_text": "By presidential mandates issued Monday night Yueh Chao-chu councillor of the ministry of foreign affairs was appointed minister to Mexico and Chang Chien Jr was appointed minister to Chile",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["Monday night"],
          "position_in_text": [2143]
        }
      ],
      "time_start": null,
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_04",
      "event_text": "The news lias been given out by the Peking Tramway company that two of the main lines of the Peking tramways will be operation on July 1.",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["on July 1"],
          "position_in_text": [2847]
        }
      ],
      "time_start": ["1924-07-01", "1924-07-01"],
      "time_end": ["1924-07-01", "1924-07-01"],
      "range": null
    },
    {
      "event_id": "1319854677_05",
      "event_text": "This seems to be the conviction of number of Chinese P's about 200 in number who held meeting in the Central Park of Peking May 15, and passed resolution that tlie government should request the British Legation to close up the British Legation Guards' Club in Mei Cha Hutung owing to intolerable disturbances and series of untoward incidents committed by its members",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 15"],
          "position_in_text": [3487]
        }
      ],
      "time_start": ["1924-05-15", "1924-05-15"],
      "time_end": ["1924-05-15", "1924-05-15"],
      "range": null
    },
    {
      "event_id": "1319854677_06",
      "event_text": "Burgess secretary of the Community Service depart ment of the Peking left for Shanghai May 15, to be away for about three weeks",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 15"],
          "position_in_text": [4331]
        }
      ],
      "time_start": ["1924-05-15", "1924-05-15"],
      "time_end": ["1924-05-15", "1924-05-15"],
      "range": null
    },
    {
      "event_id": "1319854677_07",
      "event_text": "Dr Jacob Gould Schurman the American Minister to China accompanied by Mrs Schurman left Peking May 14, for Tientsin where Dr Schurman spoke before the Tientsin Rotary Club and also to the students of the Nankai university",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 14"],
          "position_in_text": [4502]
        }
      ],
      "time_start": ["1924-05-14", "1924-05-14"],
      "time_end": ["1924-05-14", "1924-05-14"],
      "range": null
    },
    {
      "event_id": "1319854677_08",
      "event_text": "They left for Taian the next evening for sightseeing trip up the sacred mountain of Taishan and to the birthplace of Confucius at Chufu",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["the next evening"],
          "position_in_text": [4663]
        }
      ],
      "time_start": ["1924-05-15", "1924-05-15"],
      "time_end": ["1924-05-15", "1924-05-15"],
      "range": null
    },
    {
      "event_id": "1319854677_09",
      "event_text": "From Taian Mrs Schurman will return to Peking while Dr Schurman will proceed to Shang hai returning to Peking about May 20.",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["about May 20"],
          "position_in_text": [4835]
        }
      ],
      "time_start": ["1924-05-20", "1924-05-20"],
      "time_end": ["1924-05-20", "1924-05-20"],
      "range": null
    },
    {
      "event_id": "1319854677_10",
      "event_text": "General William Conner commander of the 15th Infantry at Tientsin accompanied by his aides and Mr Peck Chinese secretary of the American Legation left Peking May 12, for Loyang where they will be guests of General Wu Pei-fu for few days",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 12"],
          "position_in_text": [5059]
        }
      ],
      "time_start": ["1924-05-12", "1924-05-12"],
      "time_end": ["1924-05-12", "1924-05-12"],
      "range": null
    },
    {
      "event_id": "1319854677_11",
      "event_text": "Hiram Cleaver ex-president of the Continental Oil Company of Denver Colorado and Mrs Cleaver arrived in Peking May 14.",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["May 14"],
          "position_in_text": [5282]
        }
      ],
      "time_start": ["1924-05-14", "1924-05-14"],
      "time_end": ["1924-05-14", "1924-05-14"],
      "range": null
    },
    {
      "event_id": "1319854677_12",
      "event_text": "An unidentified messenger who refused to give the name of the sender brought package to Dr Koo's residence Thursday evening- and said that the box contained articles for the Foreign Minister's personal use",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["Thursday evening"],
          "position_in_text": [5520]
        }
      ],
      "time_start": null,
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319854677_13",
      "event_text": "On Friday afternoon Dr Koo order ed the package opened",
      "event_sources": [
        {
          "filename": "1319854677.txt",
          "time_related_expr": ["On Friday afternoon"],
          "position_in_text": [5687]
        }
      ],
      "time_start": null,
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_00",
      "event_text": "yet last week at the in Shanghai 120 women enrolled for ten days course of lectures on these subjects coming daily from 3 to 5: 30.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["last week"],
          "position_in_text": [248]
        }
      ],
      "time_start": null,
      "time_end": null,
      "range": null
    },
    {
      "event_id": "1319843498_01",
      "event_text": "Jean Alvalyn was born to Mr and Mrs Cannon at Foochow China on November 6.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on November 6"],
          "position_in_text": [2570]
        }
      ],
      "time_start": ["1917-11-06", "1917-11-06"],
      "time_end": ["1917-11-06", "1917-11-06"],
      "range": null
    },
    {
      "event_id": "1319843498_02",
      "event_text": "social evening hearts drive and dance will be held in the Municipal Service Club No 8-b Peking Road to members and their friends only on Friday November 14.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Friday November 14"],
          "position_in_text": [2650]
        }
      ],
      "time_start": ["1917-11-14", "1917-11-14"],
      "time_end": ["1917-11-14", "1917-11-14"],
      "range": null
    },
    {
      "event_id": "1319843498_03",
      "event_text": "Mrs George Fryer will be at home to her freinds at No 4 Edinburgh Road Shanghai during the second and third Fridays November 14 and 21 from 4 to 6",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["November 14 and 21"],
          "position_in_text": [2810]
        }
      ],
      "time_start": ["1917-11-14", "1917-11-14"],
      "time_end": ["1917-11-21", "1917-11-21"],
      "range": null
    },
    {
      "event_id": "1319843498_04",
      "event_text": "The announcement is made of the marriage of Dr Amy Metcalf formerly of the American Board Mission for four years in North China and Capt Albert Bowen at Tours France on October 29.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on October 29"],
          "position_in_text": [3073]
        }
      ],
      "time_start": ["1917-10-29", "1917-10-29"],
      "time_end": ["1917-10-29", "1917-10-29"],
      "range": null
    },
    {
      "event_id": "1319843498_05",
      "event_text": "At the home of the faculty of the Shanghai American School at No 147 Szechuen Road Shanghai reception was given to parents and their friends by the faculty on Tuesday afternoon Novem ber xi",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Tuesday afternoon Novem ber xi"],
          "position_in_text": [3437]
        }
      ],
      "time_start": ["1917-11-11", "1917-11-11"],
      "time_end": ["1917-11-11", "1917-11-11"],
      "range": null
    },
    {
      "event_id": "1319843498_06",
      "event_text": "The wedding took place at Hankow China on No vember 2, of John Bristow of the Standard Oil Com pany at Shanghai and Miss Frances Helen Blair at the home of Mr and Mrs Gale the ceremony being performed by Rev Littell",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on No vember 2"],
          "position_in_text": [3817]
        }
      ],
      "time_start": ["1917-11-02", "1917-11-02"],
      "time_end": ["1917-11-02", "1917-11-02"],
      "range": null
    },
    {
      "event_id": "1319843498_07",
      "event_text": "More than 400 members of the Shanghai com munity and their guests were present at the Armistice celebration at the Shanghai Club on Tuesday evening November 11.",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Tuesday evening November 11"],
          "position_in_text": [4188]
        }
      ],
      "time_start": ["1917-11-11", "1917-11-11"],
      "time_end": ["1917-11-11", "1917-11-11"],
      "range": null
    },
    {
      "event_id": "1319843498_08",
      "event_text": "plan to hold an informal dinner during the winter season to entertain the officers and men of the American warships in harbor at the Navy at No 6 Avenue Edward VII under the auspices of the American Woman's Club and the Navy was decided at their first at home held on Saturday evening November 8, at which more than 60 guests were present",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Saturday evening November 8"],
          "position_in_text": [4808]
        }
      ],
      "time_start": ["1917-11-08", "1917-11-08"],
      "time_end": ["1917-11-08", "1917-11-08"],
      "range": null
    },
    {
      "event_id": "1319843498_09",
      "event_text": "At dinner given by YangTcheng Commissioner of Foreign Affairs at the Naval Club on Saturday evening November 8, the following guests were present",
      "event_sources": [
        {
          "filename": "1319843498.txt",
          "time_related_expr": ["on Saturday evening November 8"],
          "position_in_text": [5228]
        }
      ],
      "time_start": ["1917-11-08", "1917-11-08"],
      "time_end": ["1917-11-08", "1917-11-08"],
      "range": null
    },
    {
      "event_id": "po_zh_8342_00",
      "event_text": "陳總統水扁先生今天下午前往南投縣埔里鎮參加國道六號南投段開工動土典禮，並應邀致詞。",
      "event_sources": [
        {
          "filename": "po_zh_8342.txt",
          "time_related_expr": ["今天下午"],
          "position_in_text": [8]
        }
      ],
      "time_start": ["2004-02-25", "2004-02-25"],
      "time_end": ["2004-02-25", "2004-02-25"],
      "range": null
    },
    {
      "event_id": "po_zh_8342_01",
      "event_text": "兩年前，「中二高」南投路段完工通車",
      "event_sources": [
        {
          "filename": "po_zh_8342.txt",
          "time_related_expr": ["兩年前"],
          "position_in_text": [259]
        }
      ],
      "time_start": ["2002-01-01", "2002-12-31"],
      "time_end": ["2002-01-01", "2002-12-31"],
      "range": null
    },
    {
      "event_id": "po_zh_8342_02",
      "event_text": "隨著「第二高速公路」於今年1月全線通車",
      "event_sources": [
        {
          "filename": "po_zh_8342.txt",
          "time_related_expr": ["今年1月"],
          "position_in_text": [602]
        }
      ],
      "time_start": ["2004-01-01", "2004-01-31"],
      "time_end": ["2004-01-01", "2004-01-31"],
      "range": null
    },
    {
      "event_id": "po_zh_8342_03",
      "event_text": "「高速鐵路」於明年十月開始營運通車",
      "event_sources": [
        {
          "filename": "po_zh_8342.txt",
          "time_related_expr": ["明年十月"],
          "position_in_text": [647]
        }
      ],
      "time_start": ["2005-10-01", "2005-10-31"],
      "time_end": ["2005-10-01", "2005-10-31"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_00",
      "event_text": "一九二一年考入清華官費出洋",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二一年"],
          "position_in_text": [46]
        }
      ],
      "time_start": ["1921-01-01", "1921-12-31"],
      "time_end": ["1921-01-01", "1921-12-31"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_01",
      "event_text": "一九二五年受碩士銜",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二五年"],
          "position_in_text": [139]
        }
      ],
      "time_start": ["1925-01-01", "1925-12-31"],
      "time_end": ["1925-01-01", "1925-12-31"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_02",
      "event_text": "女士已於今夏七月間取道歐洲藉以考查各國敎育狀况後始行回國",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["今夏七月間"],
          "position_in_text": [214]
        }
      ],
      "time_start": ["1927-07-01", "1927-07-31"],
      "time_end": ["1927-07-01", "1927-07-31"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_03",
      "event_text": "倩鴻女士亦爲中西女塾高材生一九二一年赴美留學",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二一年"],
          "position_in_text": [307]
        }
      ],
      "time_start": ["1921-01-01", "1921-12-31"],
      "time_end": ["1921-01-01", "1921-12-31"],
      "range": null
    },
    {
      "event_id": "SPSP192708311019_04",
      "event_text": "一九二六年春季回國",
      "event_sources": [
        {
          "filename": "SPSP192708311019.txt",
          "time_related_expr": ["一九二六年春季"],
          "position_in_text": [349]
        }
      ],
      "time_start": ["1926-03-01", "1926-05-31"],
      "time_end": ["1926-03-01", "1926-05-31"],
      "range": null
    },
    {
      "event_id": "SPSP193109022001_00",
      "event_text": "上海扶輪社本星期四午間十二時三十分、在老卡爾登舉行聚餐會",
      "event_sources": [
        {
          "filename": "SPSP193109022001.txt",
          "time_related_expr": ["本星期四午間十二時三十分"],
          "position_in_text": [10]
        }
      ],
      "time_start": ["1931-09-03", "1931-09-03"],
      "time_end": ["1931-09-03", "1931-09-03"],
      "range": null
    }
  ]
}
```