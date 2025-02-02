# Dataset Summary
This repository provides access to two different kinds of data:

Human preference data about helpfulness and harmlessness from Training a Helpful and Harmless Assistant with Reinforcement Learning from Human Feedback. These data are meant to train preference (or reward) models for subsequent RLHF training. These data are not meant for supervised training of dialogue agents. Training dialogue agents on these data is likely to lead to harmful models and this shold be avoided.
Human-generated and annotated red teaming dialogues from Red Teaming Language Models to Reduce Harms: Methods, Scaling Behaviors, and Lessons Learned. These data are meant to understand how crowdworkers red team models and what types of red team attacks are succesful or not. The data are not meant for fine-tuning or preference modeling (use the data above for preference modeling). These data are entire transcripts of conversations that are derived from the harmlessness preference modeling data described above, where only the chosen response is incorporated into the overall transcript. Furthermore, the transcripts are annotated with human and automated measurements of how harmful the overall dialogues are.


## Human preference data about helpfulness and harmlessness (PM Data)
The data are described in the paper: Training a Helpful and Harmless Assistant with Reinforcement Learning from Human Feedback. If you find the data useful, please cite the paper. The data format is very simple -- each line of the jsonl files contains a pair of texts, one "chosen" and one "rejected".

For helpfulness, the data are grouped into train/test splits in three tranches: from our base models (context-distilled 52B language models), via rejection sampling (mostly with best-of-16 sampling) against an early preference model, and a dataset sampled during our iterated "online" process.

For harmlessness, the data are only collected for our base models, but otherwise formatted in the same way.

Details about the data collection process and crowdworker population can be found in the paper, specifically in section 2 and appendix D

## Red teaming data (not PM Data)

The data are described in the paper: Red Teaming Language Models to Reduce Harms: Methods, Scaling Behaviors, and Lessons Learned. If you find the data useful, please cite the paper. At a high level these data can be examined to understand what succesful red team attempts look like.

Details about the data and data collection procedures can be found in the Datasheet in the appendix of the paper.

Each line of the jsonl file contains a dictionary with the following fields:

transcript a text transcript of a conversation between a human adversary (red team member) and an AI assistant
min_harmlessness_score_transcript a real value score of the harmlessness of the AI assistant (lower is more harmful) as obtained from a preference model
num_params number of parameters in the language model powering the AI assistant
model_type type of model powering the AI assistant
rating the red team member's rating of how successful they were at breaking the AI assistant (Likert scale, higher is more successful)
task_description a short text description written by the red team member about how they tried to red team the AI assistant
task_description_harmlessness_score a real value score of the harmlessness of the task description (lower is more harmful) as obtained from a preference model
red_team_member_id an arbitrary identifier of the red team member. one red team member can generate multiple red team attacks
is_upworker a binary indicator that is true if the red team member was from the crowd platform Upwork or false if they were from MTurk
tags a list of up to 6 tags per transcript. tags are short descriptions of the red team attempts generated by crowdworkers who reviewed red team data post-hoc. tags were only provided for a random sample of 1000 red team attempts for two of four model types.