# Dinara-Rakhimgaliyeva
игры для учителей
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Math Games for Teachers</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-color: #f9f9f9;
        }
        .hero {
            background-color: #007bff;
            color: white;
            padding: 50px 20px;
            text-align: center;
        }
        .game-card {
            border: 1px solid #ddd;
            border-radius: 8px;
            overflow: hidden;
            transition: transform 0.3s;
        }
        .game-card:hover {
            transform: scale(1.05);
        }
    </style>
</head>
<body>
    <header class="bg-primary text-white text-center py-3">
        <h1>Math Games for Teachers</h1>
        <p>Your one-stop resource for engaging math activities</p>
    </header>

    <section class="hero">
        <h2>Welcome to Math Games for Teachers!</h2>
        <p>Find fun and interactive math problems for your students!</p>
        <a href="#games" class="btn btn-light">Browse Games</a>
    </section>

    <section id="games" class="container py-5">
        <h3 class="text-center mb-4">Popular Games</h3>
        <div class="row">
            <div class="col-md-4 mb-4">
                <div class="game-card">
                    <img src="https://via.placeholder.com/300x200" alt="Game 1" class="img-fluid">
                    <div class="p-3">
                        <h5>Math Puzzle</h5>
                        <p>Challenge your students with this exciting puzzle game!</p>
                        <a href="#" class="btn btn-primary">Download</a>
                    </div>
                </div>
            </div>
            <div class="col-md-4 mb-4">
                <div class="game-card">
                    <img src="https://via.placeholder.com/300x200" alt="Game 2" class="img-fluid">
                    <div class="p-3">
                        <h5>Number Hunt</h5>
                        <p>A fun way to practice number recognition and patterns.</p>
                        <a href="#" class="btn btn-primary">Download</a>
                    </div>
                </div>
            </div>
            <div class="col-md-4 mb-4">
                <div class="game-card">
                    <img src="https://via.placeholder.com/300x200" alt="Game 3" class="img-fluid">
                    <div class="p-3">
                        <h5>Math Bingo</h5>
                        <p>An interactive game that combines math and fun!</p>
                        <a href="#" class="btn btn-primary">Download</a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="upload" class="container py-5">
        <h3 class="text-center mb-4">Upload Your Own Math Games</h3>
        <form>
            <div class="mb-3">
                <label for="gameCategory" class="form-label">Category</label>
                <select class="form-control" id="gameCategory">
                    <option value="puzzle">Puzzle</option>
                    <option value="numbers">Numbers</option>
                    <option value="bingo">Bingo</option>
                    <option value="geometry">Geometry</option>
                    <option value="algebra">Algebra</option>
                </select>
            </div>
            <div class="mb-3">
                <label for="gameTitle" class="form-label">Game Title</label>
                <input type="text" class="form-control" id="gameTitle" placeholder="Enter the title of your game">
            </div>
            <div class="mb-3">
                <label for="gameDescription" class="form-label">Description</label>
                <textarea class="form-control" id="gameDescription" rows="3" placeholder="Provide a brief description of your game"></textarea>
            </div>
            <div class="mb-3">
                <label for="gameFile" class="form-label">Upload File</label>
                <input class="form-control" type="file" id="gameFile">
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    </section>

    <section id="uploaded-games" class="container py-5">
        <h3 class="text-center mb-4">Uploaded Games</h3>
        <div id="games-list" class="list-group">
            <!-- Uploaded games will be displayed dynamically -->
        </div>
    </section>

    <footer class="bg-dark text-white text-center py-3">
        <p>&copy; 2024 Math Games for Teachers. All rights reserved.</p>
    </footer>

    <script>
        async function fetchUploadedGames() {
            const response = await fetch('/uploaded-files');
            const files = await response.json();
            const gamesList = document.getElementById('games-list');
            gamesList.innerHTML = '';

            files.forEach(file => {
                const listItem = document.createElement('div');
                listItem.className = 'list-group-item d-flex justify-content-between align-items-center';
                listItem.innerHTML = `
                    <span>${file}</span>
                    <button class="btn btn-danger btn-sm" onclick="deleteFile('${file}')">Delete</button>
                `;
                gamesList.appendChild(listItem);
            });
        }

        async function deleteFile(filename) {
            await fetch(`/delete-file/${filename}`, { method: 'DELETE' });
            fetchUploadedGames();
        }

        document.addEventListener('DOMContentLoaded', fetchUploadedGames);
    </script>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
