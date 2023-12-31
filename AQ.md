 "# 5. Algorithmic Question #" 
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