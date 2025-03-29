## OVERVIEW

Natural language (NL) requirement statements are commonly expressed in English which proves to be challenging to be comprehensible by a computer system. Therefore, expressing these statements in mathematical logic can help open up opportunities for automation. Despite its prevalence, until now, large language models (LLMs) have not been extensively utilised for mathematical logic tasks, with traditional rule-based learning being the predominant approach. Large language models are advanced artificial intelligence systems designed to comprehend and generate human-like text on a vast scale, revolutionising natural language processing tasks.

In this project, I explore and fine-tune LLMs such as Google T5 and Mistral-7B to generate mathematical logic expressions from natural language requirement statements. This entails analysis of correlations and comparison of models based on 6 selected classes, namely Implication, Rate of change, Latched, Conditional, Triggered Timed Action and Persistency, which reflect frequently occurring patterns of logic observed in embedded systems of daily use like refrigerators, cars, washing machines, and other safety critical systems.

## METHODOLOGY

In order to address the dearth of NL requirement statements availability issues, this project took a proactive approach by developing a custom dataset. The generated data were balanced across the six classes as part of the cleaning process. Leveraging transfer learning, I utilised and fine-tuned two different pre-trained LLMs and generated corresponding logic expressions. The models were further fine-tuned to generate more accurate results. Following
this, the models were tested on unseen data.

## DATASET

The dataset used in this project was meticulously crafted to encompass a variety of natural language requirement statements, which are most commonly observed logical statements in the domain of embedded systems, including electronic gadgets and safety-critical systems. The embedded systems considered here are refrigerators, washing machines, drones, vacuum cleaners, flight control systems, cars, spacecrafts, satellite communication systems and air conditioners to name a few. Broadly divided into six classes, each representing distinct logical patterns, the dataset serves as a valuable resource for training and evaluating our models. The six classes within the dataset are as follows: 

Implication: These statements indicate a causal relationship between conditions and actions. Represented by statements such as “If the air purifier's filter is removed during operation, an audible alert will be triggered.” The corresponding logic expression is “(Filter Removed during Operation) --> (Audible Alert Triggered)”

Rate of Change: These statements establish constraints on the rate of change of specific parameters. Illustrated by statements like “The rate of change of altitude shall not exceed 500 feet per minute.” The corresponding logic expression is “abs(rate of change of altitude) <= 500 feet per minute.”

Triggered Time Action: These statements define actions triggered by specific conditions within specified time frames. Represented by statements such as “If the drone's propeller blades become obstructed and the obstacle detection system is operational, the drone shall halt propeller rotation within 100 milliseconds.” The corresponding logic expression is “Triggered_Timed_Action ((Propeller blade obstruction detected on drone and Obstacle detection system operational), (Halt propeller rotation), 100 milliseconds).”

Conditional: These statements introduce conditions that dictate certain actions. Evident in statements like “During take-off, if a critical failure is detected, the take-off shall be aborted only if the current speed is less than V1.” The corresponding logic expression is “(During takeoff and critical failure detected) --> takeoff aborted --> current speed < V1.”

Persistency: These statements highlight actions that persist over defined periods of time. Showcased by statements like “If the navigation system fails to update coordinates continuously for 1 minute, the emergency beacon shall be activated.” The corresponding logic expression is “Trigger_Persists(Navigation system fails to update coordinates, Activate emergency beacon, 1 minute)”

Latched: These statements describe actions that remain in effect until explicitly deactivated. Portrayed by statements such as “If the motion sensor detects intruders, the alarm shall be permanently activated until disarmed by security personnel.” The corresponding logic expression is “Intruders detected by motion sensor --> (Alarm permanently activated globally).” 

## LLMs

GOOGLE T5: One of the variants of the T5 model, namely the 't5-base' version with 220M parameters, has been employed in this study. The data is pre-processed using the T5Tokenizer which facilitates the transformation of raw text inputs into numerical representations understandable by the model followed by padding for uniform batch processing and is trained.

MISTRAL-7B: The model specifications for the task at hand are: firstly, the Low-Rank Adaptation (LoRA) configurations were adjusted, employing a rank of 64 alongside a scaling parameter of 16. Additionally, a dropout layer with a rate of 0.1 was integrated. The model was then directly loaded onto a GPU in 4-bit precision using the NF4 type, alongside its corresponding Generation of Mathematical Intent from NL Requirements Using LLMs Jan-May 2024 13 tokenizer and was trained by passing them on to the Supervised Fine-Tuning (SFT) trainer. SFT is used for the actual fine-tuning process of language models, where the model is trained on a specific task or dataset to improve its performance for that particular use case. SFT involves providing labelled data and adjusting the model's parameters through supervised learning to optimise its performance on the given task. It allows for the adaptation of pretrained models to new tasks or domains, enhancing their effectiveness and versatility. LoRA has been incorporated to optimise the efficiency of fine-tuning by reducing computational and memory requirements, commonly employed in LLMs with a huge number of parameters.




