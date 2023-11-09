# Report

## Part 1. Plain Aggregates and Privacy

1. Kinan is a PhD student at Brown in either his 3rd or 4th year. Even if he began his doctoral program right after completing his undergraduate degree, he would be at least 25 years old. Consequently, it's likely that his musical preferences lean towards Country, Pop, Rock, or Metal. Metal, in particular, seems to be the most probable choice, given that both individuals aged 29 and 30 selected Metal as their favorite genre.

2. Kinan's personal website reveals that he enjoys Metal, a preference that aligns with the findings from the previous question. By examining his academic history on LinkedIn, it appears that he likely turned 30 years old. 

3. The color Blue seems to be the best choice, as the sole 30-year-old respondent expressed a preference for this color.

4. Since Kinan is older than 25 and has disclosed his age, his favorite sport is likely one of the following options: baseball, basketball, e-sports, or soccer.

5. Analyzing the disparities between the two datasets, we can narrow down Kinan's favorite sport to either soccer or e-sports. When considering his exact age, it becomes evident that Kinan's preference is for soccer.

## Part 2: Implementing Differential Privacy

6. When the value of ε is greater, the outcomes tend to closely match the actual values, offering limited privacy guarantees but delivering more precise and valuable data. Conversely, when ε is smaller, the level of privacy protection is heightened, and fewer details about individual data points are disclosed. However, this heightened privacy comes at the cost of diminished data utility, often resulting in numerous negative counts when ε is very small, such as 0.1 or 0.01.

7. The graph below illustrates the results when ε is set to 0.5:
![plot](dp-plot.png)

## Part 3: Differential Privacy and Composition

8. It is probable that our TA possesses over a decade of programming experience, considering that this particular group has an average age of approximately 28 or 29, which closely aligns with the TA's actual age. In contrast, the other groups all exhibit average ages that are equal to or less than 23. However, it's important to note that this inference may be incorrect if an apparently less likely group contains a significant number of data points. For instance, if a group consists of 20 individuals, with one person aged 30 while the rest are around 21-22 years old, the average age would still be 23.

9. We can deduce that there are only four students with more than a decade of programming experience, and given the limited number of students in the class around the age of 29, it follows that all these students must possess over 10 years of programming experience for the average age to remain at this elevated level.

10. The Budget class falls short in ensuring the privacy budget. Several shortcomings exist:
    - The tracking of the budget lacks cryptographic enforcement and verification. A developer could potentially alter the BudgetTracker code to disregard budget constraints or reset the budget.
    - The budget is not stored in persistent data storage and is reset every time the program runs.
    - The BudgetTracker relies on the explicit call of "check_and_update_budget()" before each query, which leaves room for developer oversight or potential access to data APIs outside of the BudgetTracker.
    - The privacy cost of each query (EPSILON) is manually configured, and underestimating it can result in overspending the true privacy budget.
    - The BudgetTracker does not prevent the correlation of multiple queries to glean more information than intended. For instance, a developer could alternate between "average" and "count" queries within the same function to extract data beyond the budget.

    A more robust approach might involve:
    - Employing cryptographic techniques to enforce privacy spending, ensuring that each query can prove it adheres to the budget.
    - Executing queries within a trusted execution environment, such as SGX enclaves, which cannot be modified or bypassed by developers.
    - Implementing an independent system for auditing and blocking queries that exceed budget limits or exhibit correlations, reducing reliance on developer self-enforcement.
    - Utilizing a dynamic system to track the true privacy cost of each query, accounting for variations based on the sensitivity of each query.
    
    The overarching idea is that privacy protection should be securely integrated into the system architecture rather than added as a superficial layer, where developers could intentionally or accidentally circumvent it. Automated enforcement throughout the pipeline is preferable to depending solely on developer discipline.