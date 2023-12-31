 # 5. Algorithmic Question
PART A
    
    def max_global_score(N, M, S, optimal_skills, athletes):
    # Create a 3D table to store the maximum scores
    dp = [[[0] * (S + 1) for _ in range(M + 1)] for _ in range(N + 1)]

    # Iterate through athletes
    for i in range(1, N + 1):
        # Iterate through roles
        for j in range(1, M + 1):
            # Iterate through remaining skills
            for k in range(S + 1):
                # Maximum score if we don't use the current athlete
                dp[i][j][k] = dp[i - 1][j][k]

                # Check if we can assign the athlete to the current role
                if k > 0 and athletes[i][1] in optimal_skills[j - 1]:
                    # Maximum score if we use the current athlete
                    dp[i][j][k] = max(dp[i][j][k], dp[i - 1][j - 1][k - 1] + athletes[i][2])

    return dp[N][M][S]

    # Input parsing
    N, M, S = map(int, input().split())
    optimal_skills = input().split()

    athletes = {}
    for _ in range(N):
     athlete_id = int(input())
     skills = [input().split() for _ in range(S)]
     athletes[athlete_id] = skills

    # Call the function and print the result
    result = max_global_score(N, M, S, optimal_skills, athletes)
    print(result)

1. This code allows Team Rome to select the best athletes for a national sports championship. Using dynamic programming, the algorithm chooses ten athletes from the given candidates based on an optimal set of skills defined by the coaches. The goal is to maximize the team's total score, considering the proficiency of each athlete in the specified skills.

2.My solutions time complexity function is O(NMS):
N represents the number of athletes.
M represents the number of roles or positions to be filled in the team.
S represents the number of skills associated with each athlete.   Because we have loop with tree ingredients. Also ı create a 3d sized table.

3. Asked to Chat-GPT for Big O Notation. It says same. Time complexity is O(N*M*S).

4. 

5.If S=1 ,it means every athlete associated with only can have one skill. We only have 0 and 1 for innermost loop. Time complexity becomes N*M because S is constant. New time complexity will be O(N*M).
