# week-5-assignment
#html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hackathon Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="style.css">
</head>
<body class="p-4 sm:p-8">

    <div class="max-w-4xl mx-auto bg-white p-6 rounded-lg shadow-xl">

        <h1 class="text-3xl sm:text-4xl font-bold text-center text-blue-700 mb-6">Hackathon 2025: Build the Future!</h1>

        <p id="hackathonStatus" class="text-lg text-center mb-8">Current Status: Registration Open! Join us for an exciting challenge.</p>

        <div id="featuredProject" class="bg-gradient-to-r from-purple-400 to-blue-500 text-white p-6 rounded-lg shadow-md flex flex-col items-center justify-center transition-all duration-500 ease-in-out">
            <h2 class="text-2xl font-semibold mb-3">Featured Project Idea</h2>
            <p class="text-center">Develop an AI-powered tool for sustainable city planning.</p>
        </div>

        <div class="text-center mt-8">
            <button id="hackathonActionButton" class="px-6 py-3 bg-green-500 text-white font-semibold rounded-lg shadow-md hover:bg-green-600 transition-colors duration-300">Update Info & Add Participant</button>
        </div>

        <div id="participantsList" class="mt-10 border-t pt-6 border-gray-200">
            <h2 class="text-2xl font-semibold mb-4 text-center">Registered Participants</h2>
            </div>

    </div>

    <script src="script.js"></script>

</body>
</html>
 #css
 body {
    font-family: 'Inter', sans-serif; /* Use Inter font */
    background-color: #f4f7f6; /* Light background */
    color: #333;
}

.added-element {
    margin-top: 15px;
    padding: 10px;
    background-color: #e9e9e9;
    border: 1px solid #ccc;
    border-radius: 4px;
}
#jss
// Wait for the DOM to be fully loaded before running the script
document.addEventListener('DOMContentLoaded', () => {

    // Get references to the HTML elements by their IDs
    const hackathonStatusElement = document.getElementById('hackathonStatus');
    const featuredProjectElement = document.getElementById('featuredProject');
    const hackathonActionButton = document.getElementById('hackathonActionButton');
    const participantsListContainer = document.getElementById('participantsList');

    // Array of possible hackathon statuses
    const statuses = [
        'Current Status: Registration Open! Join us for an exciting challenge.',
        'Current Status: Hacking in Progress! Teams are building amazing things.',
        'Current Status: Judging Phase! Submissions are being reviewed.',
        'Current Status: Winners Announced! Congratulations to the victors!',
        'Current Status: Event Concluded. See you next year!'
    ];
    let currentStatusIndex = 0;

    // Counter for added participants
    let participantCount = 0;

    // Add an event listener to the button
    hackathonActionButton.addEventListener('click', () => {

        // 1. Change text content dynamically (Hackathon Status)
        currentStatusIndex = (currentStatusIndex + 1) % statuses.length;
        hackathonStatusElement.textContent = statuses[currentStatusIndex];

        // 2. Modify CSS styles via JavaScript (Featured Project Card)
        // Toggle background gradient and maybe add a subtle border
        if (featuredProjectElement.classList.contains('from-purple-400')) {
            featuredProjectElement.classList.remove('from-purple-400', 'to-blue-500');
            featuredProjectElement.classList.add('from-green-400', 'to-teal-500');
            featuredProjectElement.style.border = '2px solid #fff'; // Add a border
        } else {
            featuredProjectElement.classList.remove('from-green-400', 'to-teal-500');
            featuredProjectElement.classList.add('from-purple-400', 'to-blue-500');
            featuredProjectElement.style.border = 'none'; // Remove border
        }

        // 3. Add or remove an element (Participant)
        if (participantCount < 5) { // Limit the number of added participants for demo
            // Add a new participant element
            participantCount++;
            const participantElement = document.createElement('div');
            // Use the 'added-element' class defined in style.css, plus some Tailwind classes
            participantElement.classList.add('added-element', 'p-3', 'bg-gray-100', 'rounded', 'mb-2');
            participantElement.textContent = `Participant #${participantCount} Joined!`;
            participantsListContainer.appendChild(participantElement);

            // Update button text
            if (participantCount === 5) {
                hackathonActionButton.textContent = 'Clear Participants';
            } else {
                 hackathonActionButton.textContent = `Add Participant (${participantCount}/5)`;
            }

        } else {
            // Remove all participant elements
            while (participantsListContainer.lastChild && participantsListContainer.lastChild.classList.contains('added-element')) {
                participantsListContainer.removeChild(participantsListContainer.lastChild);
            }
            participantCount = 0;
            hackathonActionButton.textContent = 'Update Info & Add Participant'; // Reset button text
        }
    });

}); // End of DOMContentLoaded listener
