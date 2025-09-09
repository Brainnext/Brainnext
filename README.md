<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic GitHub Profile</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #0d1117; color: #c9d1d9; }
    </style>
</head>
<body class="p-8">

    <div class="max-w-4xl mx-auto space-y-8">
        <header class="text-center space-y-4">
            <h1 class="text-5xl font-extrabold text-white">Hey, I'm [Your Name]</h1>
            <p class="text-xl text-gray-400">Welcome to my little corner of the internet.</p>
        </header>

        <section class="grid md:grid-cols-2 gap-8">
            <!-- Latest Blog Post Section -->
            <div class="bg-gray-800 rounded-lg p-6 shadow-2xl transition-transform transform hover:scale-105">
                <h2 class="text-2xl font-bold text-white mb-4">Latest Blog Post</h2>
                <div id="latest-post-content">
                    <p class="text-gray-400 animate-pulse">Fetching latest post...</p>
                </div>
            </div>

            <!-- Live Stats Section -->
            <div class="bg-gray-800 rounded-lg p-6 shadow-2xl transition-transform transform hover:scale-105">
                <h2 class="text-2xl font-bold text-white mb-4">Live GitHub Stats</h2>
                <div class="space-y-2">
                    <p id="repo-count" class="text-gray-400">Repositories: <span class="text-white font-bold">...</span></p>
                    <p id="star-count" class="text-gray-400">Total Stars: <span class="text-white font-bold">...</span></p>
                    <p id="commit-count" class="text-gray-400">Total Commits (Last Year): <span class="text-white font-bold">...</span></p>
                </div>
            </div>
        </section>

        <!-- Dynamic Content Section -->
        <section class="bg-gray-800 rounded-lg p-6 shadow-2xl transition-transform transform hover:scale-105">
            <h2 class="text-2xl font-bold text-white mb-4">Currently Working On</h2>
            <div id="current-project">
                <p class="text-gray-400 animate-pulse">Loading project details...</p>
            </div>
        </section>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const username = '[Your-GitHub-Username]';

            // Function to fetch GitHub user data
            async function fetchGitHubData() {
                try {
                    const userResponse = await fetch(`https://api.github.com/users/${username}`);
                    const userData = await userResponse.json();

                    const reposResponse = await fetch(`https://api.github.com/users/${username}/repos`);
                    const reposData = await reposResponse.json();

                    const starCount = reposData.reduce((sum, repo) => sum + repo.stargazers_count, 0);

                    document.getElementById('repo-count').innerHTML = `Repositories: <span class="text-white font-bold">${userData.public_repos}</span>`;
                    document.getElementById('star-count').innerHTML = `Total Stars: <span class="text-white font-bold">${starCount}</span>`;
                    // Note: GitHub API doesn't provide total commits directly, so we'll use a placeholder.
                    document.getElementById('commit-count').innerHTML = `Total Commits (Last Year): <span class="text-white font-bold">...</span>`;

                } catch (error) {
                    console.error('Error fetching GitHub data:', error);
                }
            }

            // Function to fetch blog post data (this is a placeholder)
            async function fetchLatestBlogPost() {
                try {
                    // Replace this with your actual blog's RSS or API endpoint
                    const mockPost = {
                        title: "How I Built My Dynamic GitHub README",
                        url: "https://yourblog.com/post-link",
                        date: "2024-05-20"
                    };

                    document.getElementById('latest-post-content').innerHTML = `
                        <a href="${mockPost.url}" target="_blank" class="text-lg font-semibold text-blue-400 hover:underline">${mockPost.title}</a>
                        <p class="text-sm text-gray-500 mt-1">${mockPost.date}</p>
                    `;
                } catch (error) {
                    console.error('Error fetching blog post:', error);
                }
            }

            // Function to fetch current project data (this is a placeholder)
            async function fetchCurrentProject() {
                try {
                    const mockProject = {
                        name: "Project Gemini",
                        description: "A collaborative writing tool built with Vue.js and Firestore.",
                        link: "https://github.com/[Your-GitHub-Username]/[Your-Project-Name]"
                    };

                    document.getElementById('current-project').innerHTML = `
                        <h3 class="text-lg font-semibold text-white">${mockProject.name}</h3>
                        <p class="text-gray-400 mt-2">${mockProject.description}</p>
                        <a href="${mockProject.link}" target="_blank" class="mt-4 inline-block text-blue-400 hover:underline">View on GitHub &rarr;</a>
                    `;
                } catch (error) {
                    console.error('Error fetching project data:', error);
                }
            }

            // Call all fetch functions
            fetchGitHubData();
            fetchLatestBlogPost();
            fetchCurrentProject();
        });
    </script>
</body>
</html>
