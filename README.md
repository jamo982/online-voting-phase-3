-- Create a database
CREATE DATABASE voting_system;

-- Switch to the created database
USE voting_system;

-- Create a table to store voting options and their votes
CREATE TABLE votes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    candidate_name VARCHAR(100) NOT NULL,
    vote_count INT DEFAULT 0
);
INSERT INTO votes (candidate_name, vote_count) VALUES
('Candidate A', 0),
('Candidate B', 0),
('Candidate C', 0);
<?php
// Connect to the database
$host = 'localhost';
$username = 'root';  // Change to your MySQL username
$password = '';      // Change to your MySQL password
$dbname = 'voting_system';

$conn = new mysqli($host, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Fetch all candidates
$sql = "SELECT * FROM votes";
$result = $conn->query($sql);
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Online Voting</title>
    <!-- Include Bootstrap CSS -->
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container">
        <h1 class="my-4 text-center">Online Voting</h1>
        <form action="vote.php" method="POST">
            <div class="form-group">
                <label for="candidate">Choose a Candidate:</label>
                <select name="candidate_id" class="form-control" required>
                    <option value="">Select a candidate</option>
                    <?php while ($row = $result->fetch_assoc()): ?>
                        <option value="<?php echo $row['id']; ?>"><?php echo $row['candidate_name']; ?></option>
                    <?php endwhile; ?>
                </select>
            </div>
            <button type="submit" class="btn btn-primary">Submit Vote</button>
        </form>
    </div>

    <!-- Include Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>

<?php
$conn->close();
?>
<?php
// Connect to the database
$host = 'localhost';
$username = 'root';  // Change to your MySQL username
$password = '';      // Change to your MySQL password
$dbname = 'voting_system';

$conn = new mysqli($host, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Fetch all candidates
$sql = "SELECT * FROM votes";
$result = $conn->query($sql);
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Online Voting</title>
    <!-- Include Bootstrap CSS -->
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container">
        <h1 class="my-4 text-center">Online Voting</h1>
        <form action="vote.php" method="POST">
            <div class="form-group">
                <label for="candidate">Choose a Candidate:</label>
                <select name="candidate_id" class="form-control" required>
                    <option value="">Select a candidate</option>
                    <?php while ($row = $result->fetch_assoc()): ?>
                        <option value="<?php echo $row['id']; ?>"><?php echo $row['candidate_name']; ?></option>
                    <?php endwhile; ?>
                </select>
            </div>
            <button type="submit" class="btn btn-primary">Submit Vote</button>
        </form>
    </div>

    <!-- Include Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>

<?php
$conn->close();
?>
<?php
// Connect to the database
$host = 'localhost';
$username = 'root';  // Change to your MySQL username
$password = '';      // Change to your MySQL password
$dbname = 'voting_system';

$conn = new mysqli($host, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Check if form is submitted
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $candidate_id = $_POST['candidate_id'];

    if ($candidate_id) {
        // Increment the vote count for the selected candidate
        $sql = "UPDATE votes SET vote_count = vote_count + 1 WHERE id = ?";
        $stmt = $conn->prepare($sql);
        $stmt->bind_param("i", $candidate_id);

        if ($stmt->execute()) {
            echo "<div class='alert alert-success'>Your vote has been successfully submitted!</div>";
        } else {
            echo "<div class='alert alert-danger'>Failed to submit your vote. Please try again.</div>";
        }
    } else {
        echo "<div class='alert alert-warning'>Please select a candidate.</div>";
    }
}

$conn->close();
?>

<a href="index.php" class="btn btn-primary mt-3">Back to Voting</a>
<?php
// Connect to the database
$host = 'localhost';
$username = 'root';  // Change to your MySQL username
$password = '';      // Change to your MySQL password
$dbname = 'voting_system';

$conn = new mysqli($host, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Fetch voting results
$sql = "SELECT * FROM votes";
$result = $conn->query($sql);
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Voting Results</title>
    <!-- Include Bootstrap CSS -->
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container">
        <h1 class="my-4 text-center">Voting Results</h1>
        <table class="table table-bordered">
            <thead>
                <tr>
                    <th>Candidate</th>
                    <th>Votes</th>
                </tr>
            </thead>
            <tbody>
                <?php while ($row = $result->fetch_assoc()): ?>
                    <tr>
                        <td><?php echo $row['candidate_name']; ?></td>
                        <td><?php echo $row['vote_count']; ?></td>
                    </tr>
                <?php endwhile; ?>
            </tbody>
        </table>
        <a href="index.php" class="btn btn-primary">Back to Voting</a>
    </div>

    <!-- Include Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.2/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>

<?php
$conn->close();
?>
