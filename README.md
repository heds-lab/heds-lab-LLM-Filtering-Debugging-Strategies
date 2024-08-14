# Title

## Initial Prompt for All Strategies
You are a well-trained Computer Science Education expert who is annotating a dataset based on students' code submissions. Usually there are 3-5 submissions in one episode. Note that when there are 5 submissions, it means there is a change between each pair of submissions 1-2, 2-3, 3-4 and 4-5. Each submission starts with "Submitted answer (x/y)", meaning x is the xth submission of a total of y submissions in the **current** episode. The **current** submission is the submission you should look at, and the **previous** submission is the one right before the **current** submission. For this task, don't concern the Starter Code provided. Here is the guideline to help you figure out the student’s debugging strategies by looking at their submission episode. Read through them carefully, review the submissions and annotate them step-by-step. You only need to go over the whole guideline ONCE following the markdown structure.

### "Strategy C":
- This only applies to fixing syntax/checkstyle errors one by one.
- Students may be fixing the exact same error but in different places and they change it to the same code, e.g. length(), utils->util.
- Note: same errors on different lines are considered as ONE error instead of multiple.

### "Strategy F":
- This only applies to fixing test errors.
- Students are purposefully fixing the code step by step.
- Debugging based on smaller, targeted changes and knowledge of code that is known to work.
- Adding a small-to-medium-sized chunk of code that was syntactically similar to the code that already existed.

### "Strategy A":
- Utilize System.out.println or similar to output intermediate results.
- Adjustments to the code may follow based on these outputs.
- Excluded if print statements are explicitly part of the question's requirements.
- Effective only if students view the output at least once; errors preventing output display disqualify it as tracing.
- Can co-occur with other debugging strategies within the same code submission.

### "Strategy D": 
- This only applied to fixing syntax and checkstyle errors
- process-oriented, when students are fixing different, multiple syntaxt or checkstyle errors on one submission
- Note: the SAME errors on different lines are considered as ONE error instead of multiple
- Can co-occur with other debugging strategies within the same code submission.

### "Strategy B":
- Involves significantly changing the approach or logic to solve the problem, not just making minor edits or fixes.
- Some indicators are: using a new algorithm or logic; major changes to the code's core structure or flow; a shift in strategy, not just minor edits.
- Can co-occur with other strategies

### "Strategy E":
- This only applied to fixing for Syntax or checkstyle errors
- tinkering behavior might be more systematic and constant; some changes with no base; students seem not knowing what they are doing by simply reacting to errors without thinking; random and usually unproductive changes
- Usually we don't take students' behaviors as tinkering even they may seem unproductive. This is because students may take a detour to find the solution, or they may try something out to find a solution

### "Strategy G":
- This only applied to fixing for Test or semantic errors
- "Tinkering: test" is a debugging approach where students make arbitrary or guess-based changes to code in response to test errors, without a clear understanding or logical strategy. This method is characterized by:
- Arbitrary Changes
- Lack of Logical Progression
- Experimental Adjustments
- Absence of Reasoning
- tinkering behavior might be more systematic and constant; some changes with no base; students seem not knowing what they are doing by simply reacting to errors without thinking; random and usually unproductive changes
- Usually we don't take students' behaviors as tinkering even they may seem unproductive. This is because students may take a detour to find the solution, or they may try something out to find a solution

### "Strategy N":
- Activities not directly related to debugging, like merely completing the solution.
- Cannot be labeled as a specific strategy if there are signs of multiple strategies, but they don't satisfy any of the rules listed above.

### Overall labeling notes (IMPORTANT!):
- Label an entire episode as a set of strategies. While your rationale may include details about strategies used between individual pairs of submissions, your main annotation should represent the overall strategy for the entire episode.
- The patterns are for the changes between submissions, not for the submissions themselves.
- Strategy "Strategy A" and "Strategy B" should be labeled as long as the strategy occurs AT LEAST ONCE in an episode.
- Strategy "Strategy C", "Strategy F", "Strategy D", "Strategy E" and "Strategy G" should be labeled only if the strategy occurs AT LEAST TWO TIMES on the changes between submissions in an episode.
- "Strategy N" would not occur with any other strategies.

Below I will give you the coding question (requirements) and the students' submissions. Based on the hierarchical instructions, give me your reasoning on the student's debugging strategies using the same way of reason given above, and then output both the rationales and the strategies used between each pair of the consecutive submission in a JSON dictionaries as below. Make sure you output the rationales and strategies for all submission pairs! More than one strategy can be present in each pair of submissions. Try to be concise and precise.

{{"1_2_rationale": "...", "1_2_strategy": ["..."],
"2_3_rationale": "...", "2_3_strategy": ["..."],
"3_4_rationale": "...", "3_4_strategy": ["..."],
"4_5_rationale": "...", "4_5_strategy": ["..."]}}

## Finalized Prompt (with Expert Decision Map)
You are a well-trained Computer Science Education expert who is annotating a dataset based on students' code submissions. Usually there are 3-5 submissions in one episode. Note that when there are 5 submissions, it means there is a change between each pair of submissions 1-2, 2-3, 3-4 and 4-5. Each submission starts with "Submitted answer (x/y)", meaning x is the xth submission of a total of y submissions in the **current** episode. The **current** submission is the submission you should look at, and the **previous** submission is the one right before the **current** submission. For this task, don't concern the Starter Code provided. Here is the guideline to help you figure out the student’s debugging strategies by looking at their submission episode. Read through them carefully, review the submissions and annotate them step-by-step. You only need to go over the whole guideline ONCE following the markdown structure.

Look at the **previous** submission, if there is no error presented in the **previous** submission errors:
    # then the **current** submission presents the label of "Strategy M", no matter if there are changes or not.

If there's any kind of errors presented in the **previous** submission:

    # Look at the **current** submission, are there any System.out.println or similar code presented in the submission?
        ## If there is, Check the question to see if there are any examples or requirements that ask students to print the results.
        ## If there is NO such requirements or examples, then the **current** submission presents the strategy of "Strategy A" only if it fits the following:
            ### the students use code tracing, or
            ### the submission presents System.out.println or similar codes to print out intermediate or final outputs, and 
            ### the submission presents no syntax or checkstyle errors, so the printed output can be viewed by the students.
        ## Else, if there ARE such requirements or examples, then the **current** submission presents the strategy of "Strategy A" only if it fits the following:
            ### the students use code tracing, or
            ### the submission presents System.out.println or similar codes to print out intermediate or final outputs, and 
            ### the submission presents no syntax or checkstyle errors, so the printed output can be viewed by the students, and
            ### the codes for printing is not part of the requirements or examples.

    # Else, if there isn’t any tracing behaviors, check to see if are there changes involve editing or replacing the majority of the codes presented in this submission?
        ## If there is, check the changes in the **current** submission and compare it with the **previous** submission. If the **previous** submission contains any types of errors, then it presents the strategy "Strategy B" only if it fits the following cases:
            ### the changes involve deleting, editing or replacing the **majority** of the codes, and
            ### the changes does not repeat the same solution from the **previous** submission.

        ## Else, if there isn’t any major editing of the codes, look at the **previous** submission’s errors. Which kind of errors does this submission have?
            ### If there are only syntax or checkstyle errors presented in the **previous** submission errors:
                #### then it presents the strategy "Strategy C" only if it fits the following cases:
                    ##### if the changes occur on only one line targeting any errors, or 
                    ##### if there is only one syntax error in the previous submission, and the changes are targeting it, or 
                    ##### if there is only one type of checkstyle error in the previous submission, and the changes are targeting it, or
                    ##### if the changes occur on multiple lines, but are targeting exactly 1 syntax error from the **previous** submission, or
                    ##### if the changes occur on multiple lines, but are targeting exactly 1 type of checkstyle errors from the **previous** submission, and
                    #### the changes may or may not introduce any new errors.
                #### Else, if the above cases don’t apply, then it presents the strategy "Strategy D" only if it fits the following cases:
                    #### if the changes occur on different lines, and are targeting 2 or more syntax errors from the **previous** submission,or
                    #### if the changes occur on different lines, and are targeting 2 or more types of checkstyle errors from the **previous** submission, and 
                    #### the changes may or may not introduce any new errors.
                #### Else, if the above cases don’t apply, then it presents the negative strategy "Strategy E" only if it fits the following cases:
                    #### if the students are tinkering the codes but the changes are baseless and/or unproductive and/or useless, which means they are not directly or indirectly resolving the syntax errors, and they are not part of the solutions to the syntax error, or
                    #### if the students replace some codes with different version of the codes with the same functions, so the submission is basically the same, and
                    #### the changes may or may not introduce any new errors, and 
                    #### Usually we don't assume students are tinkering even if they are taking a detour.
                #### Else, if there's no Syntax nor checkstyle error, there shouldn't be Strategy C, D or E.

            ### If there are only test errors presented in the **previous** submission errors:
                #### Then it presents the strategy "Strategy F" only if it fits the following cases:
                    ##### the changes only involve editing or replacing small chunks of codes, and
                    ##### the changes try to target the test errors from the **previous** submission, and
                    ##### the changes may directly or indirectly resolve the test errors, or
                    ##### they can be the test error's solution, or
                    ##### they can be a step towards the test error's solution, and 
                    #### the changes may or may not introduce any new errors.
                ####  Else, if the above don’t apply, then the **current** submission presents the strategy "Strategy G" only if it fits the following cases:
                    ##### the students are tinkering the codes but the changes are attempted to fix a test error from the **previous** submission, but the changes are baseless and/or unproductive and/or useless, which means they are not directly or indirectly resolving the test errors, and they are not part of the solutions to the test error.
                    #### The students replace some codes with different version of the codes with the same functions, so the submission is basically the same, and
                    #### the changes may or may not introduce any new errors, and
                    #### Usually we don't assume students are tinkering even if they are taking a detour.
                #### Else, if there's no test error, there shouldn't be Strategy F or G.
        ## Else, if none of these applies, then it might be "Strategy N".

Below I will give you the coding question (requirements) and the students' submissions. Based on the hierarchical instructions, give me your reasoning on the student's debugging strategies using the same way of reason given above, and then output both the rationales and the strategies used between each pair of the consecutive submission in a JSON dictionaries as below. Make sure you output the rationales and strategies for all submission pairs! More than one strategy can be present in each pair of submissions. Try to be concise and precise.

{{"1_2_rationale": "...", "1_2_strategy": ["..."],
"2_3_rationale": "...", "2_3_strategy": ["..."],
"3_4_rationale": "...", "3_4_strategy": ["..."],
"4_5_rationale": "...", "4_5_strategy": ["..."]}}

## Individual Strategy Prompts
### Strategy - Tracing
You are a well-trained Computer Science Education expert who is annotating a dataset based on students' code submissions. Usually there are 3-5 submissions in one episode. Note that when there are 5 submissions, it means there is a change between each pair of submissions 1-2, 2-3, 3-4 and 4-5. Each submission starts with "Submitted answer (x/y)", meaning x is the xth submission of a total of y submissions in the **current** episode. The **current** submission is the submission you should look at, and the **previous** submission is the one right before the **current** submission. For this task, don't concern the Starter Code provided. Here is the guideline to help you figure out the student’s debugging strategies by looking at their submission episode. Read through them carefully, review the submissions and annotate them step-by-step. You only need to go over the whole guideline ONCE following the markdown structure.


If there's any kind of errors presented in the previous submission and there are System.out.println or similar code segments in the current submission:

    # Look at the **current** submission, are there any System.out.println or similar code presented in the submission? If there is, Check the question to see if there are any examples or requirements that ask students to print the results.
        ## If there is NO such requirements, then the **current** submission presents the strategy of "Strategy A" only if it fits the following:
            ### the students use code tracing, or
            ### the submission presents System.out.println or similar codes to print out intermediate or final outputs, and 
            ### the submission presents no syntax or checkstyle errors, so the printed output can be viewed by the students.
        ## Else, if there ARE such requirements, then the **current** submission presents the strategy of "Strategy A" only if it fits the following:
            ### the students use code tracing, or
            ### the submission presents System.out.println or similar codes to print out intermediate or final outputs, and 
            ### the submission presents no syntax or checkstyle errors, so the printed output can be viewed by the students, and
            ### the codes for printing is not part of the requirements or examples.
        ## Else, label the current submission as "Other".


Below I will give you the coding question (requirements) and the students' submissions. Based on the hierarchical instructions, give me your reasoning on the student's debugging strategies using the same way of reason given above, and then output both the rationales and the strategies used between each pair of the consecutive submission in a JSON dictionaries as below. Make sure you output the rationales and strategies for all submission pairs! More than one strategy can be present in each pair of submissions. Try to be concise and precise.

{{"1_2_rationale": "...", "1_2_strategy": ["..."],
"2_3_rationale": "...", "2_3_strategy": ["..."],
"3_4_rationale": "...", "3_4_strategy": ["..."],
"4_5_rationale": "...", "4_5_strategy": ["..."]}}

### Strategy - Starting Over
You are a well-trained Computer Science Education expert who is annotating a dataset based on students' code submissions. Usually there are 3-5 submissions in one episode. Note that when there are 5 submissions, it means there is a change between each pair of submissions 1-2, 2-3, 3-4 and 4-5. Each submission starts with "Submitted answer (x/y)", meaning x is the xth submission of a total of y submissions in the **current** episode. The **current** submission is the submission you should look at, and the **previous** submission is the one right before the **current** submission. For this task, don't concern the Starter Code provided. Here is the guideline to help you figure out the student’s debugging strategies by looking at their submission episode. Read through them carefully, review the submissions and annotate them step-by-step. You only need to go over the whole guideline ONCE following the markdown structure.

For each submission in an episode, if the previous submission is Starter Code, skip it and move to the next submission in the episode; if the previous submission is not Starter Code, look at the **previous** submission:

    # if there's any kind of errors presented in the **previous** submission, check the changes in the **current** submission and compare it with the **previous** submission. The **current** submission presents the strategy "Strategy B" only if it fits the following cases:
        ## the changes involve editing or replacing the **majority** of the codes, and
        ## The changes started from the beginning of the submission, and
        ## the changes does not re-use the same solution from the **previous** submission, and
        ## the changes should NOT just be an addition of new chunk of codes, and
        ## the changes should NOT just be a deletion of new chunk of codes.
Else, label it as "Other".

Below I will give you the coding question (requirements) and the students' submissions. Based on the hierarchical instructions, give me your reasoning on the student's debugging strategies using the same way of reason given above, and then output both the rationales and the strategies used between each pair of the consecutive submission in a JSON dictionaries as below. Make sure you output the rationales and strategies for all submission pairs! More than one strategy can be present in each pair of submissions. Try to be concise and precise.

{{"1_2_rationale": "...", "1_2_strategy": ["..."],
"2_3_rationale": "...", "2_3_strategy": ["..."],
"3_4_rationale": "...", "3_4_strategy": ["..."],
"4_5_rationale": "...", "4_5_strategy": ["..."]}}

### Strategy - All
