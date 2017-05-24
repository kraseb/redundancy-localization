# Evaluation Data for Redundancy Localization

This repository contains data for the evaluation of redundancy localization in pairs of short texts. The dataset accompanies the following paper:

-  Title: "Redundancy Localization for the Conversationalization of Unstructured Responses"
-  Authors: (anonymized)
-  Unpublished

## The Task

The task of redundancy localization is to understand when a given sub-passage is redundant with what is mentioned in the context. More formally, given a context passage and a target passage, and further given a segmentation of the target passage into spans, the task is to rank the spans according to the extent to which their content is covered by the context passage. A particular application of models for this task is in dialogues between digital assistants and human users. Here, the assistant should avoid to reiterate on statements from the dialogue history, since this can result in the dialogue sounding redundant and incoherent.

## The Data

The dataset was constructed from pairs of potentially redundant passages from Wikipedia, which were segmented into sub-passages and presented to human raters for manual redundancy assessment.

The collection of passages was guided by a need for text pairs with various degrees of semantic overlap; we employed a passage-retrieval system for the purpose of text selection. We picked a random set of 1200 fact-seeking questions and retrieved corresponding passages from Wikipedia. After this step, the questions were discarded. We selected the top-scoring passage as the *context passage* and paired it with a low-scoring one from further down the result list (*the target passage*). Then, the target passage was heuristically split into *spans*, roughly corresponding to verb-governed phrases.

We asked three raters per item to select for each span one out of three labels: non-redundant, partially redundant, and fully redundant, depending on the degree of which the content of a sub-passage is covered by the context. We aggregated the rating by mapping the categorical labels to a numeric scale and averaging the scores. In the experiments of our paper, we used 200 examples for development purposes (partition 'validation') and the remaining 1000 items as a test dataset (partition 'test'). Both dataset partitions are encoded in CSV.

In the provided files, each sample (row) is a pair of passages along with the URLs of the Wikipedia pages from which they were retrieved. The target passage's spans are indicated by their respective offsets and lengths. Each span is associated with the redundancy assessment by the raters, ranging from 0.0 (fully redundant) to 2.0 (non-redundant).

**Columns:**

* context_passage : This is the passage against which the individual spans are compared.
* target_passage : This passage is segmented into spans.
* context_url : URL of Wikipedia article from which we extracted the context passage.
* target_url : URL of Wikipedia article from which we extracted the target passage.

Then follow groups of three columns each, with `[DIGIT]` running from 0 to 8 (inclusive). Per-span information can be empty for `[DIGIT]` >= 2; there are at least three spans in each target passage.

* span`[DIGIT]`_offset : Position of first character in this span.
* span`[DIGIT]`_length : Length of span.
* span`[DIGIT]`_redundancy_score : Redundancy assessment of raters.

## Example from Dataset (1)

column | content
--- | ---
context_passage | James was selected with the first overall pick in the 2003 NBA draft by the Cleveland Cavaliers.
target_passage | LeBron James, who was drafted by the Cleveland Cavaliers in 2003, left for the Miami Heat in 2010, but re-signed with the Cleveland Cavaliers on July 11, 2014.
context_url | https://en.wikipedia.org/wiki/LeBron_James
target_url | https://en.wikipedia.org/wiki/2003_NBA_draft
span0_offset | 0
span0_length | 21
span0_redundancy_score | 1.666667
span1_offset | 22
span1_length | 43
span1_redundancy_score | 0
span2_offset | 66
span2_length | 36
span2_redundancy_score | 2
span3_offset | 103
span3_length | 56
span3_redundancy_score | 2

The target passage has the following spans, with the second span being the most redundant one with respect to the context passage above:

1. LeBron James, who was 
2. drafted by the Cleveland Cavaliers in 2003, 
3. left for the Miami Heat in 2010, but 
4. re-signed with the Cleveland Cavaliers on July 11, 2014.

## Example from Dataset (2)

column | content
--- | ---
context_passage | At the 78th Academy Awards, Brokeback Mountain was nominated for the Academy Award for Best Picture and won three awards for Best Director, Best Adapted Screenplay, and Original Score.
target_passage | The film was nominated for eight Academy Awards, the most nominations at the 78th Academy Awards, where it won three: Best Director, Best Adapted Screenplay, and Best Original Score, while losing Best Picture.
context_url | https://en.wikipedia.org/wiki/List_of_accolades_received_by_Brokeback_Mountain
target_url | https://en.wikipedia.org/wiki/Brokeback_Mountain
span0_offset | 0
span0_length | 12
span0_redundancy_score | 2
span1_offset | 13
span1_length | 84
span1_redundancy_score | 2
span2_offset | 98
span2_length | 19
span2_redundancy_score | 0
span3_offset | 118
span3_length | 91
span3_redundancy_score | 0.333333

Here, the third span is the most redundant one.

1. The film was 
2. nominated for eight Academy Awards, the most nominations at the 78th Academy Awards, 
3. where it won three: 
4. Best Director, Best Adapted Screenplay, and Best Original Score, while losing Best Picture.

## Example from Dataset (3)

column | content
--- | ---
context_passage | Stefka Kostadinova (Bulgaria) has held the women's world record at 2.09 m (6 ft 101⁄4 in) since 1987, also the longest-held record in the event.
target_passage | Kostadinova is the reigning world record holder in the women's high jump at 2.09 m, which she jumped during the 1987 World Championships in Athletics in Rome. Her world record is one of the oldest in modern athletics.
context_url | https://en.wikipedia.org/wiki/High_jump
target_url | https://en.wikipedia.org/wiki/Stefka_Kostadinova
span0_offset | 0
span0_length | 83
span0_redundancy_score | 0.666667
span1_offset | 84
span1_length | 74
span1_redundancy_score | 1.333333
span2_offset | 159
span2_length | 58
span2_redundancy_score | 1

In this example, are spans all similarly redundant, with the first one sounding slightly more repetitive than the others, according to the raters:

1. Kostadinova is the reigning world record holder in the women's high jump at 2.09 m, 
2. which she jumped during the 1987 World Championships in Athletics in Rome. 
3. Her world record is one of the oldest in modern athletics.

## License

The data is licensed under the Creative Commons Attribution-ShareAlike 3.0 license. For more details: https://creativecommons.org/licenses/by-sa/3.0/us/ .

## Contact

- (anonymized)

