# Source Form — Structural Reference

This is the complete field-by-field structure of the paper form Project
Hope digitizes. Any future prompt, schema, or UI description should
reference this file instead of re-describing the form — this is the
single source of truth for what data the system actually needs to
capture.

**No institution name is included here or anywhere else in this repo.**

## Program name
| Language | Text |
|---|---|
| Arabic | رحلة الأمل |
| English | Road of Hope / Journey of Hope |
| French | Le Chemin de l'Espoir |

## Form title
| Language | Text |
|---|---|
| Arabic | بطاقة متابعة طفل مريض بالسرطان ضمن برنامج "رحلة الأمل" |
| English | Cancer Patient Child Follow-up Card, within the "Road of Hope" Program |
| French | Fiche de suivi d'un enfant atteint de cancer, dans le cadre du programme « Le Chemin de l'Espoir » |

## Form subtitle (context line)
| Language | Text |
|---|---|
| Arabic | في مصلحة أورام الأطفال بمستشفى [مؤسسة] |
| English | At the Pediatric Oncology Department of [institution] |
| French | Au service d'oncologie pédiatrique de [établissement] |

Note: the institution name is intentionally left as a placeholder here
and must never be filled in inside this repository.

## Recorder field
The form has a single line at the top for the person filling it out,
labeled "المتطوعة" (grammatically feminine "the volunteer" — the form
consistently uses feminine grammatical forms throughout, likely
reflecting that most people filling it out have been women; worth noting
but not necessarily binding for how the app addresses users). Per the
corrected role naming for this project, this corresponds to the
**Intern** role (see root README), though a Psychologist may also fill
this in a session.

---

## Section 1 — General Information About the Child
`معلومات عامة عن الطفل` / General Information About the Child / Informations générales sur l'enfant

| Field (Arabic) | Field (English) | Field (French) | Type | Options |
|---|---|---|---|---|
| الاسم واللقب | First and last name | Nom et prénom | Text | — |
| العمر | Age | Âge | Number | — |
| (gender, same line as age) | Sex | Sexe | Radio | ذكر/Male/Masculin, أنثى/Female/Féminin |
| الولاية | Province (Wilaya) | Wilaya | Text | — |
| رقم الغرفة | Room number | Numéro de chambre | Text/Number | — |
| القسم (المستوى الدراسي) | School level/grade | Niveau scolaire | Text | — |
| التحق بالمدرسة | Enrolled in school | Scolarisé | Radio | نعم/Yes/Oui, لا/No/Non |
| متابعة من طرف | Followed up by | Suivi par | Radio/Text | معلمة المدرسة/School teacher/Enseignante, الأم أو شخص آخر/Mother or other person/Mère ou autre personne |
| تاريخ الانضمام للبرنامج | Program join date | Date d'adhésion au programme | Date | — |

## Section 2 — Educational Follow-up
`المتابعة التربوية والتعليمية` / Educational Follow-up / Suivi éducatif et pédagogique

| Field (Arabic) | Field (English) | Field (French) | Type | Options |
|---|---|---|---|---|
| الدرس | Lesson/subject | Leçon/matière | Text | — |
| مستوى الفهم والاستيعاب | Comprehension level | Niveau de compréhension | Radio | ممتاز/Excellent/Excellent, جيد/Good/Bien, متوسط/Average/Moyen, يحتاج دعم/Needs support/A besoin de soutien |
| المشاركة في الأنشطة | Activity participation | Participation aux activités | Radio | نشط/Active/Actif, متوسط/Moderate/Moyen, قليل/Low/Faible |
| القدرة على التركيز والانتباه | Focus/attention ability | Capacité de concentration | Radio | جيدة/Good/Bonne, متوسطة/Average/Moyenne, ضعيفة/Weak/Faible |
| المهارات اللغوية (نطق، مفردات...) | Language skills (pronunciation, vocabulary...) | Compétences linguistiques (prononciation, vocabulaire...) | Radio | جيدة/Good/Bonnes, تحتاج دعم/Needs support/Ont besoin de soutien |
| المهارات الحركية الدقيقة (الكتابة، القص، التلوين) | Fine motor skills (writing, cutting, coloring) | Motricité fine (écriture, découpage, coloriage) | Radio | جيدة/Good/Bonnes, تحتاج دعم/Needs support/Ont besoin de soutien |
| المهارات الاجتماعية (تفاعل، احترام الدور...) | Social skills (interaction, turn-taking...) | Compétences sociales (interaction, respect du tour...) | Radio | جيدة/Good/Bonnes, تحتاج دعم/Needs support/Ont besoin de soutien |

## Section 3 — Psychological & Emotional Follow-up
`المتابعة النفسية والعاطفية` / Psychological & Emotional Follow-up / Suivi psychologique et émotionnel

| Field (Arabic) | Field (English) | Field (French) | Type | Options |
|---|---|---|---|---|
| الحالة المزاجية أثناء النشاط | Mood during activity | Humeur pendant l'activité | Radio | هادئ/Calm/Calme, متقلب/Variable/Changeante, حزين/Sad/Triste, فرح/Happy/Joyeuse |
| التفاعل مع الزملاء والمتطوعات | Interaction with peers and volunteers/interns | Interaction avec les pairs et les bénévoles | Radio | جيد جدًا/Very good/Très bonne, جيد/Good/Bonne, ضعيف/Weak/Faible |
| الحاجة إلى دعم نفسي إضافي | Need for additional psychological support | Besoin de soutien psychologique supplémentaire | Radio + conditional text | نعم/Yes/Oui (with explanation field), لا/No/Non |

## Section 4 — Health Follow-up
`المتابعة الصحية والنفسية للطفل` / Health Follow-up for the Child / Suivi sanitaire de l'enfant

| Field (Arabic) | Field (English) | Field (French) | Type | Options |
|---|---|---|---|---|
| الحالة العامة أثناء النشاط | General condition during activity | État général pendant l'activité | Radio | مستقرة/Stable/Stable, متعبة/Tired/Fatigué, يحتاج راحة/Needs rest/A besoin de repos |
| ملاحظات طبية مهمة | Important medical notes | Notes médicales importantes | Free text | Example prompts on the form: treatment day, appetite loss, general fatigue, behavior change |

## Section 5 — Volunteer/Intern & Teacher Notes
`ملاحظات المتطوعة / المعلمة` / Volunteer/Intern & Teacher Notes / Notes du bénévole / de l'enseignante

| Field (Arabic) | Field (English) | Field (French) | Type |
|---|---|---|---|
| الحالة النفسية للمتطوعة بعد الجلسة | Psychological state of the volunteer/intern after the session | État psychologique du bénévole après la séance | Free text |
| التوصيات للأسبوع القادم | Recommendations for next week | Recommandations pour la semaine prochaine | Free text |

## Section 6 — Remote/At-Home Activity (conditional section)
`إذا هناك نشاط عن بعد` / If There Is a Remote Activity / S'il y a une activité à distance

| Field (Arabic) | Field (English) | Field (French) | Type | Options |
|---|---|---|---|---|
| السبب | Reason | Raison | Radio | ضعف المناعة/Weak immunity/Immunodépression, علاج في البيت/Home treatment/Traitement à domicile |
| النشاط أو الدرس | Activity or lesson | Activité ou leçon | Free text | — |
| الاستجابة | Response/engagement | Réponse/engagement | Free text | — |

---

## Notes for implementation
- Sections 2–6 together correspond to what the rest of the project docs
  call **a single session**: one patient can have many of these session
  records over time.
- Section 1 (General Information) is patient-level data, captured once
  and updated as needed — not repeated per session.
- Section 6 is conditional — it should only appear/apply when a session
  involves remote/at-home activity rather than an in-person one.
- All radio/checkbox option sets above should be treated as fixed
  enumerations in the schema (not free text) except where marked "Free
  text" or "conditional text."
- French translations here are a reasonable working translation for
  planning purposes — they should be reviewed by a French-speaking staff
  member before being used as actual UI copy, the same way the final
  Arabic/English UI copy should be reviewed by someone at the
  institution before launch.
