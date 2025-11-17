DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Med School Compass | Pre-Med Analysis</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Configure Tailwind to use Inter font and define custom colors -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        'med-blue': '#10529A', // Primary Medical Blue
                        'med-teal': '#007B80', // Secondary Teal for accents
                        'med-bg': '#F7F9FB',   // Light background for clean look
                        'success-green': '#00B894',
                    }
                }
            }
        }
    </script>
    <style>
        /* Ensuring smooth transitions for modern feel */
        .stat-card {
            transition: all 0.3s ease-in-out;
            box-shadow: 0 10px 30px -10px rgba(16, 82, 154, 0.15); /* Soft blue shadow */
        }
        /* Style for the dropdown (Select) */
        #schoolSelect {
            appearance: none;
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%2310529A' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: right 1rem center;
            background-size: 1.5em;
        }
    </style>
</head>
<body class="bg-med-bg min-h-screen flex items-center justify-center p-4 font-sans">

    <!-- Main Application Container -->
    <div class="w-full max-w-xl bg-white rounded-xl overflow-hidden shadow-2xl border border-gray-100">

        <!-- Header -->
        <header class="bg-med-blue p-6 text-white text-center rounded-t-xl">
            <h1 class="text-3xl font-extrabold tracking-tight">Med School Compass</h1>
            <p class="mt-1 text-med-bg text-sm">Targeted Insights for Your Pre-Med Journey</p>
        </header>

        <!-- Content Area -->
        <main class="p-6 md:p-8 space-y-8">

            <!-- School Selection Dropdown -->
            <div class="space-y-3">
                <label for="schoolSelect" class="block text-lg font-semibold text-gray-700">Select Your Pre-Med School:</label>
                <select id="schoolSelect" onchange="updateSchoolData()" class="w-full p-3 pr-10 border-2 border-med-blue text-med-blue rounded-lg bg-white focus:ring-2 focus:ring-med-teal focus:border-med-teal transition duration-150 shadow-inner text-base cursor-pointer">
                    <option value="" disabled selected>-- Choose an Institution --</option>
                    <option value="JHU">Johns Hopkins University</option>
                    <option value="HARVARD">Harvard University</option>
                    <option value="DUKE">Duke University</option>
                    <option value="UPENN">University of Pennsylvania</option>
                    <option value="STANFORD">Stanford University</option>
                    <option value="NYU">NYU Grossman School of Medicine</option>
                </select>
            </div>

            <!-- Results Card (Hidden until selection) -->
            <div id="resultsCard" class="stat-card p-6 bg-white border border-med-teal rounded-xl hidden space-y-6">

                <!-- School and Target Med School Info -->
                <div>
                    <h2 id="currentSchoolName" class="text-2xl font-bold text-med-blue mb-1"></h2>
                    <p class="text-gray-500 text-sm">Target Affiliated Medical School: <span id="targetMedSchool" class="font-medium text-med-teal"></span></p>
                </div>

                <!-- Statistics Grid -->
                <div class="grid grid-cols-3 gap-4 text-center">
                    <div class="p-4 bg-med-bg rounded-lg border-b-4 border-med-teal">
                        <p class="text-xs text-gray-500 font-medium uppercase">Median GPA</p>
                        <p id="medianGPA" class="text-2xl font-extrabold text-gray-800 mt-1">N/A</p>
                    </div>
                    <div class="p-4 bg-med-bg rounded-lg border-b-4 border-med-teal">
                        <p class="text-xs text-gray-500 font-medium uppercase">Median MCAT</p>
                        <p id="medianMCAT" class="text-2xl font-extrabold text-gray-800 mt-1">N/A</p>
                    </div>
                    <div class="p-4 bg-med-bg rounded-lg border-b-4 border-med-teal">
                        <p class="text-xs text-gray-500 font-medium uppercase">Med School Accept Rate*</p>
                        <p id="acceptanceRate" class="text-2xl font-extrabold text-gray-800 mt-1">N/A</p>
                    </div>
                </div>

                <!-- Profile Analysis -->
                <div class="border-t pt-4 border-gray-200">
                    <h3 class="flex items-center text-xl font-semibold text-gray-800 mb-2">
                        <svg class="w-6 h-6 mr-2 text-success-green" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                        Competitive Profile Analysis
                    </h3>
                    <p id="profileTip" class="text-gray-600 leading-relaxed text-sm"></p>
                </div>

                <p class="text-xs text-gray-400 italic mt-4">*Rates are self-reported or estimated for students successfully advised through the pre-health track, not the general applicant rate.</p>

            </div>
            
            <!-- Default Motivational Card -->
            <div id="defaultCard" class="p-6 text-center bg-med-blue/50 text-white rounded-xl shadow-lg">
                <svg class="mx-auto w-12 h-12 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M12 20.894V17m-3 1.5h6m-12 0A17.965 17.965 0 0112 11c3.15 0 6.136 1.04 8.5 2.894"></path></svg>
                <p class="mt-3 text-lg font-semibold">Select a school above to view the required academic metrics for success.</p>
                <p class="text-sm text-white/80">Every journey to the white coat starts with strong preparation!</p>
            </div>

        </main>
    </div>

    <script>
        // Sample data based on competitive med school admissions (aggregated and simplified)
        const schoolData = {
            JHU: {
                name: "Johns Hopkins University",
                medSchool: "Johns Hopkins School of Medicine",
                gpa: "3.94",
                mcat: "521",
                acceptance: "85%",
                tip: "JHU focuses heavily on research and clinical exposure. To be competitive, engage in significant laboratory research and secure strong letters of recommendation from science faculty."
            },
            HARVARD: {
                name: "Harvard University",
                medSchool: "Harvard Medical School",
                gpa: "3.93",
                mcat: "519",
                acceptance: "95%",
                tip: "The Harvard Pre-Med Advising program is exceptional. Focus not just on grades, but demonstrating intellectual vitality, leadership, and a commitment to health equity through extracurriculars."
            },
            DUKE: {
                name: "Duke University",
                medSchool: "Duke University School of Medicine",
                gpa: "3.90",
                mcat: "519",
                acceptance: "80%",
                tip: "Duke values a balance of research and clinical service. Ensure you have high-quality shadowing experiences and a meaningful capstone project in your major."
            },
            UPENN: {
                name: "University of Pennsylvania",
                medSchool: "Perelman School of Medicine",
                gpa: "3.92",
                mcat: "522",
                acceptance: "78%",
                tip: "UPenn encourages students to pursue diverse interests. A highly competitive application will combine stellar academics with humanities or policy-related clinical experiences."
            },
            STANFORD: {
                name: "Stanford University",
                medSchool: "Stanford Medicine",
                gpa: "3.89",
                mcat: "518",
                acceptance: "75%",
                tip: "As a premier West Coast institution, demonstrate significant commitment to innovation and technology in medicine. Volunteer locally and participate in Stanford's robust health research ecosystem."
            },
            NYU: {
                name: "NYU Pre-Health Track",
                medSchool: "NYU Grossman School of Medicine (Tuition Free)",
                gpa: "3.96",
                mcat: "522",
                acceptance: "4.9%", // General acceptance rate is lower, focusing on high stats
                tip: "While the med school is tuition-free, the admission stats are extremely high. Focus on achieving the top possible academic metrics and compelling New York-based clinical experience."
            }
        };

        const selectElement = document.getElementById('schoolSelect');
        const resultsCard = document.getElementById('resultsCard');
        const defaultCard = document.getElementById('defaultCard');

        function updateSchoolData() {
            const selectedKey = selectElement.value;

            // Hide the default card and show the results card
            defaultCard.classList.add('hidden');
            resultsCard.classList.remove('hidden');

            if (selectedKey && schoolData[selectedKey]) {
                const data = schoolData[selectedKey];

                // Update the DOM elements with the selected school's data
                document.getElementById('currentSchoolName').textContent = data.name;
                document.getElementById('targetMedSchool').textContent = data.medSchool;
                document.getElementById('medianGPA').textContent = data.gpa;
                document.getElementById('medianMCAT').textContent = data.mcat;
                document.getElementById('acceptanceRate').textContent = data.acceptance;
                document.getElementById('profileTip').textContent = data.tip;

            } else {
                // Should not happen if select options are linked to data, but for safety:
                resultsCard.classList.add('hidden');
                defaultCard.classList.remove('hidden');
            }
        }
    </script>
</body>
</html>
