# GitHub Action Workflow File (.github/workflows/youtube-readme-update.yml)
name: Update YouTube Section in README

on:
  schedule:
    # Runs every hour at the start of the hour
    - cron: '0 * * * *'
  workflow_dispatch:  # Allows manual triggering from the Actions tab

jobs:
  update-readme:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      # ------- CHOOSE ONE OF THE FOLLOWING TWO SECTIONS (SIMPLE LIST or YOUTUBE CARDS) -------

      # --- SECTION 1: SIMPLE LIST (Uses gautamkrishnar/blog-post-workflow) ---
      - name: Get latest YouTube videos (Simple List)
        uses: gautamkrishnar/blog-post-workflow@v3
        with:
          feed_list: "https://www.youtube.com/feeds/videos.xml?channel_id=YOUR_CHANNEL_ID"  # <--- REPLACE WITH YOUR CHANNEL ID
          max_post_count: 5  # Optional: Adjust the number of videos
          template: " - [{title}]({link})\\n" # optional: define a template for a cleaner look

      # --- SECTION 2: YOUTUBE CARDS (Uses DenverCoder1/github-readme-youtube-cards) ---
      # - name: Generate YouTube Cards  #Uncomment to use YouTube Cards
      #   uses: DenverCoder1/github-readme-youtube-cards@main #Uncomment to use YouTube Cards
      #   with:    #Uncomment to use YouTube Cards
      #     channel_id: YOUR_CHANNEL_ID  # <--- REPLACE WITH YOUR CHANNEL ID     #Uncomment to use YouTube Cards
      #     youtube_api_key: ${{ secrets.YOUTUBE_API_KEY }} # Required for some features (e.g., video duration) #Uncomment to use YouTube Cards
      #     max_title_lines: 2  # Optional: Customize the appearance     #Uncomment to use YouTube Cards
      #     show_duration: true    #Uncomment to use YouTube Cards
      #     commit_message: "docs(readme): Update YouTube cards"  #Uncomment to use YouTube Cards
      #     readme_path: README.md  #Uncomment to use YouTube Cards
      #     output_only: false    #Uncomment to use YouTube Cards
      #     output_type: markdown   #Uncomment to use YouTube Cards

      # ------- END CHOOSE ONE OF THE TWO SECTIONS -------

      - name: Commit and push changes
        uses: stefanzweifel/git-auto-commit-action@v5
        with:
          commit_message: "Update README with latest YouTube videos"
          branch: main  # Or your default branch name
