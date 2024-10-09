<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WEB API</title>
    <style>
        .container {
      width: 400px;
      margin: 100px auto;
      padding: 20px;
      border: 1px solid #ddd;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      text-align: center;
    }
    ul {
      list-style-type: none;
      padding: 0;
    }
    li {
      margin: 10px 0;
    }
    a {
      text-decoration: none;
      color: #007bff;
    }
    </style>
</head>
<body>
    <div class="container">
        <form id="githubForm">
          <input type="text" id="username" placeholder="Github username..." />
          <button type="submit">Submit</button>
        </form>
      </div>
  <script>
     const getRepos = async (username) => {
      try {
        const response = await fetch('https://api.github.com/users/' + username + '/repos');
        const repos = await response.json();
        displayRepos(repos);
      } catch (error) {
        console.error('Error:', error);
      }
    }
    function displayRepos(repos) {
      const repoList = document.createElement('ul');
      repos.forEach(repo => {
        const listItem = document.createElement('li');
        const link = document.createElement('a');
        link.href = repo.html_url;
        link.textContent = repo.name;
        link.target = "_blank"; // Open in new tab
        listItem.appendChild(link);
        repoList.appendChild(listItem);
      });
      document.querySelector('.container').appendChild(repoList);
    }
    document.getElementById('githubForm').addEventListener('submit', async function(event) {
      event.preventDefault();
      const username = document.getElementById('username').value;
      document.querySelector('.container').innerHTML = `
        <form id="githubForm">
          <input type="text" id="username" placeholder="Github username..." />
          <button type="submit">Submit</button>
         </form>
        `;
      await getRepos(username);
    });
  </script>
    
</body>
</html>
