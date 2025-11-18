[EMR 29.html.html](https://github.com/user-attachments/files/23611539/EMR.29.html.html)
<!DOCTYPE Posted HTML>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Butler University Clinical Note</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; background-color: #f0f2f5; }
        /* MODIFIED H1 STYLE - Font size changed to 40pt */
        h1 { 
            text-align: center; 
            color: navy; 
            font-size: 40pt !important; /* SET TO 40pt */
            font-weight: 900 !important; 
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }
        /* NEW DISCLAIMER STYLE */
        .disclaimer {
            text-align: center;
            color: #991b1b; /* Dark red for caution */
            font-size: 12pt; /* SET TO 12pt */
            margin-bottom: 30px;
            font-style: italic;
            padding: 10px;
            border: 1px solid #fca5a5; /* Light red border */
            background-color: #fef2f2; /* Very light red background */
            border-radius: 6px;
        }
        /* ADDED STYLE TO FORCE NEW LINE IN DISCLAIMER P TAG */
        .disclaimer p {
            margin: 0;
            line-height: 1.5;
        }
        h2 { border-bottom: 2px solid #3b82f6; padding-bottom: 8px; color: #1e3a8a; font-size: 1.5rem; }
        h3 { font-size: 1.1rem; color: #1e40af; margin-top: 1.5rem; margin-bottom: 0.5rem; border-left: 4px solid #60a5fa; padding-left: 8px;}
        label { font-weight: bold; color: #374151; }
        .med-type-label { font-weight: normal; margin-right: 10px; } /* For med radio buttons */
        input[type="text"], input[type="date"], input[type="time"], textarea, select {
            width: 100%; padding: 8px; margin-top: 5px; box-sizing: border-box;
            border: 1px solid #d1d5db; border-radius: 6px; transition: border-color 0.2s;
        }
        input[type="text"]:focus, input[type="date"]:focus, input[type="time"]:focus, textarea:focus, select:focus {
            outline: none; border-color: #3b82f6; box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.4);
        }
        input:required:invalid, textarea:required:invalid { border-color: #fca5a5; }
        input[readonly] { background-color: #e5e7eb; cursor: not-allowed; }
        textarea { 
            resize: none; /* Disable manual resize */
            min-height: 80px; 
            overflow-y: hidden; /* Hide scrollbar */
        }
        #hpi { min-height: 240px; }
        .section { margin-bottom: 30px; background-color: white; padding: 24px; border-radius: 8px; box-shadow: 0 1px 3px rgba(0,0,0,0.1); }
        .ros-buttons button {
            margin: 5px 5px 0 0; padding: 6px 12px; border: 1px solid #666;
            background-color: white; cursor: pointer; border-radius: 16px;
            transition: all 0.2s; font-size: 0.9em;
        }
        .state-positive { background-color: #dc2626 !important; color: white; border-color: #dc2626 !important; }
        .state-negative { background-color: #16a34a !important; color: white; border-color: #16a34a !important; }
        .state-none { background-color: white !important; color: black; }
        .add-line-btn {
            margin-top: 10px; padding: 8px 16px; cursor: pointer;
            background-color: #2563eb; color: white; border: none;
            border-radius: 6px; font-weight: 600; transition: background-color 0.2s;
        }
        .add-line-btn:hover { background-color: #1d4ed8; }
        .remove-line-btn {
            padding: 4px 10px; cursor: pointer; background-color: #ef4444; color: white;
            border: none; border-radius: 4px; font-weight: 500; margin-left: 10px;
        }
        .hidden { display: none; }
        .ros-key { font-size: 0.9em; color: #555; margin-top: 5px; padding: 8px; background-color: #f3f4f6; border-radius: 6px; }
    </style>
</head>
<body class="p-4 md:p-8">
    <div class="max-w-4xl mx-auto">
        <div id="save-status" class="fixed top-2 right-2 bg-green-100 text-green-800 text-sm font-medium me-2 px-2.5 py-0.5 rounded-full" style="display: none; transition: opacity 0.5s;"></div>

        <h1>Butler University Clinical Note</h1>

        <div class="disclaimer">
            <p>Disclaimer: This clinical note tool is to be used for simulated patient encounters only.<br>Do not input any protected health information.</p>
        </div>

        <form id="emr-form">

            <div class="section">
                <h2>Encounter & Identifying Data</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-4">
                    <div>
                        <label for="encounter-date">Encounter Date:</label>
                        <input type="date" id="encounter-date" name="encounter_date" onpaste="return false;">
                    </div>
                    <div>
                        <label for="patient-name">Name:</label>
                        <input type="text" id="patient-name" name="patient_name" onpaste="return false;">
                    </div>
                    <div>
                        <label for="patient-dob">DOB:</label>
                        <input type="date" id="patient-dob" name="patient_dob" onpaste="return false;">
                    </div>
                    <div>
                        <label for="patient-age">Age:</label>
                        <input type="text" id="patient-age" name="patient_age" readonly onpaste="return false;">
                    </div>
                    <div>
                        <label for="patient-gender">Gender:</label>
                        <select id="patient-gender" name="patient_gender" onpaste="return false;">
                            <option value="">--Select--</option>
                            <option value="male">Male</option>
                            <option value="female">Female</option>
                            <option value="non-binary">Non-binary</option>
                            <option value="other">Other</option>
                            <option value="prefer-not-to-say">Prefer not to say</option>
                        </select>
                    </div>
                </div>
            </div>

            <div class="section">
                <h2>Chief Complaint</h2>
                <input type="text" id="chief-complaint" name="chief_complaint" onpaste="return false;">
            </div>

            <div class="section">
                <h2>History of Present Illness (HPI)</h2>
                <textarea id="hpi" name="hpi" onpaste="return false;"></textarea>
            </div>

            <div class="section">
                <h2>Past Medical History (PMH)</h2>
                <textarea id="pmh" name="past_medical_history" onpaste="return false;" rows="10"></textarea>
            </div>

            <div class="section">
                <h2>Medications</h2>
                <div id="medication-container" class="space-y-4"></div>
                <button type="button" class="add-line-btn" onclick="addMedication()">+ Add Medication</button>
            </div>

            <div class="section">
                <h2>Social History (SH)</h2>
                <textarea id="sh" name="social_history" onpaste="return false;" rows="10"></textarea>
            </div>

            <div class="section">
                <h2>Family History (FH)</h2>
                <textarea id="fh" name="family_history" onpaste="return false;"></textarea>
            </div>

            <div class="section">
                <h2>Review of Systems (ROS)</h2>
                <div id="ros-container" class="mt-4 space-y-6">
                    <textarea id="ros-narrative" name="ros_narrative_full" rows="10" onpaste="return false;"></textarea>
                </div>
            </div>

            <div class="section">
                <h2>Physical Exam</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 mt-4">
                    <div><label for="pe-temp">Temp (°F):</label><input type="text" id="pe-temp" name="pe_temp" onpaste="return false;"></div>
                    <div><label for="pe-hr">HR (bpm):</label><input type="text" id="pe-hr" name="pe_hr" onpaste="return false;"></div>
                    <div><label for="pe-rr">RR (bpm):</label><input type="text" id="pe-rr" name="pe_rr" onpaste="return false;"></div>
                    <div><label for="pe-bp">BP (mmHg):</label><input type="text" id="pe-bp" name="pe_bp" onpaste="return false;"></div>
                    <div><label for="pe-o2">O2 (%):</label><input type="text" id="pe-o2" name="pe_o2" onpaste="return false;"></div>
                    <div><label for="pe-height">Height (in):</label><input type="text" id="pe-height" name="pe_height" onpaste="return false;"></div>
                    <div><label for="pe-weight">Weight (lbs):</label><input type="text" id="pe-weight" name="pe_weight" onpaste="return false;"></div>
                    <div class="lg:col-span-1"><label for="pe-bmi">BMI (kg/m²):</label><input type="text" id="pe-bmi" name="pe_bmi" readonly onpaste="return false;"></div>
                </div>
                <div id="physical-exam-container" class="mt-6 space-y-4">
                    <textarea id="pe-narrative" name="pe_narrative_full" rows="10" onpaste="return false;"></textarea>
                </div>
            </div>

            <div class="section">
                <h2>Labs / Diagnostic Studies</h2>
                <div id="labs-container" class="space-y-4"></div>
                <button type="button" class="add-line-btn" onclick="addLabStudy()">+ Add Lab/Study</button>
            </div>


            <div class="section">
                <h2>Assessment & Plan</h2>
                <div id="ap-group-container" class="mt-4 space-y-8">
                    </div>
                <button type="button" class="add-line-btn" onclick="addDiagnosisGroup()">+ Add Diagnosis</button>
            </div>
            <div class="section">
                <h2>Signature & Attestation</h2>
                    <div>
                        <label for="signature-name">Student Name, Credential:</label>
                        <input type="text" id="signature-name" name="signature_name" placeholder="e.g., John Smith, PA-S" required onpaste="return false;">
                    </div>
                    <div class="mt-4">
                        <label for="academic-attestation">Academic Integrity Attestation:</label>
                        <textarea id="academic-attestation" name="academic_attestation" placeholder="By completing this form, I attest that the content is my own original work. I have adhered to the program's academic integrity policy and only utilized approved resources." required onpaste="return false;"></textarea>
                    </div>
            </div>

            <div class="my-6 flex justify-between">
                <button type="button" id="export-button" class="bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded-lg shadow-md transition-transform transform hover:scale-105">
                    Save Note
                </button>
                <button type="reset" id="clear-form-button" class="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg shadow-md transition-transform transform hover:scale-105">
                    Clear Form & Saved Data
                </button>
            </div>
            </form>
    </div>

<script>
// --- CONFIGURATION ---
// ROS and Physical Exam configurations are no longer used for structure, but kept for reference
const rosSystems = {
    "General": ["Fever", "Chills", "Fatigue", "Weakness", "Appetite Change", "Weight Change", "Night Sweats"],
    // ... all other ROS systems removed from array to reduce script size
};
const physicalExamSystems = ["General", "Skin/Hair/Nails", "HEENT", "Lymphatics", "Cardiovascular", "Pulmonary", "Abdomen", "Genitourinary / Rectal", "Musculoskeletal", "Neurological", "Psychiatric"]; 
// --- END CONFIGURATION ---

let medicationCounter = 0;
let apGroupCounter = 0; 

// --- INITIALIZATION & BUILDER FUNCTIONS ---
document.addEventListener('DOMContentLoaded', () => {
    // === NEW LOGIC: Clear form and storage on every load ===
    clearFormAndStorage(false); 
    // =======================================================
    
    document.getElementById('patient-dob').addEventListener('change', calculateAge);
    document.getElementById('pe-height').addEventListener('input', calculateBMI);
    document.getElementById('pe-weight').addEventListener('input', calculateBMI);
    document.getElementById('export-button').addEventListener('click', exportNote);
    document.getElementById('clear-form-button').addEventListener('click', () => clearFormAndStorage(true)); 

    const form = document.getElementById('emr-form');
    form.addEventListener('input', debounce(saveForm, 500));
    
    // Auto-resize for all textareas and add onpaste="return false;"
    document.querySelectorAll('textarea').forEach(textarea => {
        textarea.setAttribute('onpaste', 'return false;');
        textarea.addEventListener('input', () => autoResize(textarea));
    });
    // Add onpaste="return false;" to all text/date/time inputs and selects.
    document.querySelectorAll('input[type="text"], input[type="date"], input[type="time"], select').forEach(input => {
        if(!input.hasAttribute('readonly')) {
            input.setAttribute('onpaste', 'return false;');
        }
    });

    // === NEW LOGIC FOR AUTO-FILLING PLACEHOLDER (ONLY FOR ATTESTATION) ===
    setPlaceholderAsValue('academic-attestation');
    // =======================================================
});

function addMedication() {
    medicationCounter++;
    const container = document.getElementById('medication-container');
    const entryDiv = document.createElement('div');
    entryDiv.className = 'med-entry p-3 bg-gray-50 rounded';
    entryDiv.innerHTML = `
        <div class="grid grid-cols-1 md:grid-cols-5 gap-2 items-center">
            <input type="text" name="med_name[]" onpaste="return false;">
            <input type="text" name="med_dose[]" onpaste="return false;">
            <input type="text" name="med_route[]" onpaste="return false;">
            <input type="text" name="med_freq[]" onpaste="return false;">
            <input type="text" name="med_indication[]" onpaste="return false;">
        </div>
        <div class="mt-2 flex items-center justify-between">
            <div class="med-type-group">
                <label class="med-type-label"><input type="radio" name="med_type_${medicationCounter}" value="Rx" checked> Rx</label>
                <label class="med-type-label"><input type="radio" name="med_type_${medicationCounter}" value="OTC"> OTC</label>
                <label class="med-type-label"><input type="radio" name="med_type_${medicationCounter}" value="Supplements"> Supplement</label>
            </div>
            <button type="button" class="remove-line-btn" onclick="this.closest('.med-entry').remove()">X Remove</button>
        </div>
    `;
    container.appendChild(entryDiv);
}

// --- DYNAMIC ASSESSMENT/PLAN GROUP FUNCTIONS ---
function removeApGroup(buttonElement) {
    buttonElement.closest('.ap-group').remove();
    updateApGroupNumbers();
    saveForm();
}

function updateApGroupNumbers() {
    const groups = document.querySelectorAll('.ap-group');
    groups.forEach((group, index) => {
        const newNumber = index + 1;
        group.querySelector('h3').textContent = `Diagnosis #${newNumber}`;
        group.id = `ap-group-${newNumber}`;
    });
    apGroupCounter = groups.length; 
}

function addDiagnosisGroup() {
    apGroupCounter++;
    const container = document.getElementById('ap-group-container');
    const groupDiv = document.createElement('div');
    groupDiv.className = 'ap-group border border-blue-300 p-4 rounded-lg bg-blue-50 shadow-md';
    groupDiv.id = `ap-group-temp`;
    
    groupDiv.innerHTML = `
        <div class="flex justify-between items-center mb-4 border-b border-blue-200 pb-2">
            <h3 class="font-bold text-lg text-blue-800">Diagnosis #${apGroupCounter}</h3> 
            <button type="button" class="remove-line-btn" onclick="removeApGroup(this)">X Remove Group</button>
        </div>

        <label class="font-semibold text-gray-700 block mt-2">Diagnosis</label>
        <input type="text" name="ap_diagnosis[]" class="mb-4" required onpaste="return false;">

        <label class="font-semibold text-gray-700 block mt-4">Medical Decision-Making (MDM)</label>
        <textarea name="ap_mdm[]" rows="4" onpaste="return false;"></textarea>

        <label class="font-semibold text-gray-700 block mt-4">Plan (for this Diagnosis)</label>
        <textarea name="ap_plan[]" rows="4" onpaste="return false;"></textarea>
    `;
    
    container.appendChild(groupDiv);
    
    groupDiv.querySelectorAll('textarea').forEach(textarea => {
        textarea.addEventListener('input', () => autoResize(textarea));
        autoResize(textarea);
    });
    
    updateApGroupNumbers(); 
}
// --- END DYNAMIC ASSESSMENT/PLAN GROUP FUNCTIONS ---

/* <![CDATA[ */
function autoResize(element) {
    element.style.height = 'auto';
    element.style.height = (element.scrollHeight) + 'px';
}

function setPlaceholderAsValue(elementId) {
    const el = document.getElementById(elementId);
    if (!el) return;

    function handler() {
        if (!el.value && el.placeholder) {
            el.value = el.placeholder;
            el.placeholder = '';
            autoResize(el);
            el.removeEventListener('focus', handler); 
        }
    }

    el.addEventListener('focus', handler);
    
    el.addEventListener('blur', () => {
        if (!el.value.trim() && el.placeholder === '') {
            el.placeholder = "By completing this form, I attest that the content is my own original work. I have adhered to the program's academic integrity policy and only utilized approved resources.";
            el.addEventListener('focus', handler);
        }
    });
}

// NOTE: buildRos and buildPhysicalExam removed as they are now single text areas in HTML
// The original `buildRos` and `buildPhysicalExam` functions are no longer needed 
// because the elements are now hardcoded as single textareas in the HTML.

function addLabStudy() {
    const container = document.getElementById('labs-container');
    const entryDiv = document.createElement('div');
    entryDiv.className = 'lab-study-entry p-2 bg-gray-50 rounded space-y-2';
    const today = new Date().toISOString().slice(0,10);
    entryDiv.innerHTML = `<div class="grid grid-cols-3 gap-2"><input type="date" name="lab_date[]" value="${today}" class="col-span-1 p-2 border rounded" onpaste="return false;"><input type="text" name="lab_name[]" class="col-span-2 p-2 border rounded" onpaste="return false;"></div><div><textarea name="lab_result[]" class="w-full p-2 border rounded" rows="2" onpaste="return false;"></textarea></div><button type="button" class="remove-line-btn" onclick="this.closest('.lab-study-entry').remove()">X Remove Study</button>`;
    entryDiv.querySelector('textarea').addEventListener('input', (e) => autoResize(e.target));
    container.appendChild(entryDiv);
}

function calculateAge() {
    const dobInput = document.getElementById('patient-dob').value;
    if (dobInput) {
        const dob = new Date(dobInput);
        const ageDifMs = Date.now() - dob.getTime();
        const ageDate = new Date(ageDifMs);
        document.getElementById('patient-age').value = Math.abs(ageDate.getUTCFullYear() - 1970);
    }
}
function calculateBMI() {
    const heightIn = parseFloat(document.getElementById('pe-height').value);
    const weightLbs = parseFloat(document.getElementById('pe-weight').value);
    const bmiEl = document.getElementById('pe-bmi');
    if (heightIn > 0 && weightLbs > 0) {
        const bmi = (weightLbs / (heightIn * heightIn)) * 703;
        bmiEl.value = bmi.toFixed(2);
    } else {
        bmiEl.value = '';
    }
}
const FORM_STORAGE_KEY = 'mockEmrFormData';
let saveTimeout;
function debounce(func, delay) {
    return function(...args) {
        clearTimeout(saveTimeout);
        saveTimeout = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}
function saveForm() {
    const form = document.getElementById('emr-form');
    const formData = new FormData(form);
    const data = {};
    for (const [key, value] of formData.entries()) {
        if (key.endsWith('[]') || key.startsWith('med_type_') || key.startsWith('ap_')) {
            if (!data[key]) data[key] = [];
            data[key].push(value);
        } else {
            data[key] = value;
        }
    }
    localStorage.setItem(FORM_STORAGE_KEY, JSON.stringify(data));
    const statusEl = document.getElementById('save-status');
    statusEl.textContent = 'Progress Saved!';
    statusEl.style.display = 'inline-block';
    statusEl.style.opacity = '1';
    setTimeout(() => {
        statusEl.style.opacity = '0';
        setTimeout(()=> { statusEl.style.display = 'none'; }, 500);
    }, 2000);
}
function loadForm() {
    const savedData = localStorage.getItem(FORM_STORAGE_KEY);
    if (!savedData) return;
    const data = JSON.parse(savedData);
    const form = document.getElementById('emr-form');
    
    // Reset counters (No need to call buildRos/buildPE as they are static now)
    medicationCounter = 0;
    apGroupCounter = 0;
    
    // Re-add dynamic fields based on saved data counts
    if(data['med_name[]']) data['med_name[]'].forEach(() => addMedication());
    if(data['lab_date[]']) data['lab_date[]'].forEach(() => addLabStudy());
    
    // Load Assessment/Plan Groups
    if (data['ap_diagnosis[]']) {
        data['ap_diagnosis[]'].forEach(() => addDiagnosisGroup()); 
    }


    for (const key in data) {
        const elements = form.elements[key];
        if (elements) {
            if (elements.constructor === RadioNodeList) { 
                const value = Array.isArray(data[key]) ? data[key][0] : data[key];
                if (value) {
                    for (const radio of elements) {
                        if (radio.value === value) {
                            radio.checked = true;
                            break; 
                        }
                    }
                }
            } else if (elements.constructor === NodeList || Array.isArray(elements)) {
                    elements.forEach((el, index) => {
                        if (data[key] && data[key][index] !== undefined) {
                            if (el.type === 'checkbox') el.checked = !!data[key][index];
                            else el.value = data[key][index];
                        }
                    });
            } else if (elements.type === 'checkbox') {
                elements.checked = !!data[key];
            } else {
                elements.value = data[key];
            }
        }
    }
    calculateAge();
    calculateBMI();
    document.querySelectorAll('textarea').forEach(textarea => {
        if (textarea.value) {
            autoResize(textarea);
        }
    });
}
// MODIFIED clearFormAndStorage
function clearFormAndStorage(askConfirmation = true) {
    let shouldClear = true;
    if (askConfirmation) {
        shouldClear = confirm("Are you sure you want to clear the entire form? This will also remove all saved data.");
    }
    
    if (shouldClear) {
        localStorage.removeItem(FORM_STORAGE_KEY); 
        
        document.getElementById('emr-form').reset();
        
        // Clear all dynamic containers
        document.getElementById('medication-container').innerHTML = '';
        document.getElementById('labs-container').innerHTML = '';
        document.getElementById('ap-group-container').innerHTML = '';
        
        // Reset counters
        medicationCounter = 0;
        apGroupCounter = 0;
        
        // Re-run auto-resize
        document.querySelectorAll('textarea').forEach(textarea => autoResize(textarea));
        
        // Re-enable the setPlaceholderAsValue on focus after a hard reset
        setPlaceholderAsValue('academic-attestation');
        document.getElementById('academic-attestation').placeholder = "By completing this form, I attest that the content is my own original work. I have adhered to the program's academic integrity policy and only utilized approved resources.";
    }
}
function exportNote() {
    const sigNameInput = document.getElementById('signature-name');
    const attestationInput = document.getElementById('academic-attestation'); 

    if (sigNameInput.value.trim() === '' || attestationInput.value.trim() === '') {
        alert('Please complete the Student Name and Academic Integrity Attestation fields before exporting.');
        return;
    }

    const form = document.getElementById('emr-form');
    const data = new FormData(form);
    const formDataObject = {};
    for (const [key, value] of data.entries()) {
        if (key.endsWith('[]') || key.startsWith('med_type_') || key.startsWith('ap_')) {
            if (!formDataObject[key]) formDataObject[key] = [];
            formDataObject[key].push(value);
        } else {
            formDataObject[key] = value;
        }
    }

    let htmlContent = `
        <html>
        <head>
            <title>Butler University Clinical Note - ${formDataObject['patient_name'] || 'Untitled'}</title>
            <style>
                body { font-family: Arial, sans-serif; margin: 40px; }
                h1 { text-align: center; color: navy; font-size: 30pt; margin-bottom: 5px; }
                h2 { border-bottom: 2px solid #3b82f6; padding-bottom: 5px; color: #1e3a8a; font-size: 18pt; margin-top: 30px; }
                h3 { font-size: 14pt; color: #1e40af; margin-top: 15px; margin-bottom: 5px; border-left: 3px solid #60a5fa; padding-left: 8px;}
                p { margin-top: 5px; margin-bottom: 5px; line-height: 1.4; white-space: pre-wrap; }
                .disclaimer-print { 
                    text-align: center;
                    color: #991b1b;
                    font-size: 10pt;
                    margin-bottom: 20px;
                    font-style: italic;
                    padding: 8px;
                    border: 1px solid #fca5a5;
                    background-color: #fef2f2;
                    border-radius: 4px;
                }
                .data-field { margin-left: 20px; }
                .med-entry { margin-left: 20px; border-bottom: 1px dashed #ccc; padding-bottom: 5px; margin-top: 5px;}
                .lab-entry { margin-left: 20px; border-bottom: 1px dashed #ccc; padding-bottom: 5px; margin-top: 5px;}
            </style>
        </head>
        <body>
        `;

    // 1. Title and Disclaimer
    htmlContent += `<h1>Butler University Clinical Note</h1>
                    <div class="disclaimer-print">Disclaimer: This clinical note tool is to be used for simulated patient encounters only.<br>Do not input any protected health information.</div>
                    `;


    // Helper function for adding sections
    const addSection = (title, content, rawHtml = false) => {
        if (content && (typeof content === 'string' ? content.trim() : (Array.isArray(content) ? content.length > 0 : true))) {
            htmlContent += `<h2>${title}</h2>`;
            if (rawHtml) {
                htmlContent += content;
            } else if (typeof content === 'function') {
                htmlContent += content();
            } else {
                // Replace newlines with <br> for narrative fields
                htmlContent += `<p>${String(content).trim().replace(/\n/g, '<br>')}</p>`;
            }
        }
    };

    // 2. Encounter & Identifying Data
    addSection('Encounter & Identifying Data', () => {
        let c = '<div class="data-field">';
        c += `<p><strong>Name:</strong> ${formDataObject['patient_name'] || 'N/A'}</p>`;
        c += `<p><strong>DOB:</strong> ${formDataObject['patient_dob'] || 'N/A'}</p>`;
        c += `<p><strong>Age:</strong> ${formDataObject['patient_age'] || 'N/A'}</p>`;
        c += `<p><strong>Gender:</strong> ${formDataObject['patient_gender'] || 'N/A'}</p>`;
        c += `<p><strong>Date:</strong> ${formDataObject['encounter_date'] || 'N/A'}</p>`;
        c += '</div>';
        return c;
    }, true);

    // 3. Chief Complaint
    addSection('Chief Complaint', formDataObject['chief_complaint']);

    // 4. HPI
    addSection('History of Present Illness (HPI)', formDataObject['hpi']);

    // 5. PMH
    addSection('Past Medical History (PMH)', formDataObject['past_medical_history']);
    
    // 6. Medications
    addSection('Medications', () => {
        const names = formDataObject['med_name[]'] || [];
        if (!names.some(n => n.trim())) return null;

        let c = '';
        names.forEach((name, i) => {
            if (name.trim()) {
                const dose = formDataObject['med_dose[]'][i] || 'N/A';
                const route = formDataObject['med_route[]'][i] || 'N/A';
                const freq = formDataObject['med_freq[]'][i] || 'N/A';
                const indication = formDataObject['med_indication[]'][i] || 'N/A';
                
                let type = '';
                const typeKey = Object.keys(formDataObject).find(k => k.startsWith('med_type_') && Array.isArray(formDataObject[k]) && formDataObject[k].length > i);
                if (typeKey) {
                    type = ` - (${formDataObject[typeKey][i]})`;
                }

                c += `<p class="med-entry"><strong>${name}</strong>${type}: ${dose} ${route} ${freq}. Indication: ${indication}</p>`;
            }
        });
        return c;
    });

    // 7. Social History
    addSection('Social History (SH)', formDataObject['social_history']);

    // 8. Family History
    addSection('Family History (FH)', formDataObject['family_history']);

    // 9. Review of Systems
    addSection('Review of Systems (ROS)', formDataObject['ros_narrative_full']);

    // 10. Physical Exam
    addSection('Physical Exam', () => {
        let c = '<div class="data-field"><h3>Vitals & Measurements</h3>';
        let hasVitals = false;
        if (formDataObject['pe_temp']) { c += `<p><strong>Temp:</strong> ${formDataObject['pe_temp']} °F</p>`; hasVitals = true; }
        if (formDataObject['pe_hr']) { c += `<p><strong>HR:</strong> ${formDataObject['pe_hr']} bpm</p>`; hasVitals = true; }
        if (formDataObject['pe_rr']) { c += `<p><strong>RR:</strong> ${formDataObject['pe_rr']} bpm</p>`; hasVitals = true; }
        if (formDataObject['pe_bp']) { c += `<p><strong>BP:</strong> ${formDataObject['pe_bp']} mmHg</p>`; hasVitals = true; }
        if (formDataObject['pe_o2']) { c += `<p><strong>O2:</strong> ${formDataObject['pe_o2']} %</p>`; hasVitals = true; }
        if (formDataObject['pe_height']) { c += `<p><strong>Height:</strong> ${formDataObject['pe_height']} in</p>`; hasVitals = true; }
        if (formDataObject['pe_weight']) { c += `<p><strong>Weight:</strong> ${formDataObject['pe_weight']} lbs</p>`; hasVitals = true; }
        if (formDataObject['pe_bmi']) { c += `<p><strong>BMI:</strong> ${formDataObject['pe_bmi']} kg/m²</p>`; hasVitals = true; }
        c += '</div>';

        // Add the consolidated physical exam narrative
        if (formDataObject['pe_narrative_full']?.trim()) {
            c += `<h3>Physical Exam Narrative</h3><p>${formDataObject['pe_narrative_full'].trim().replace(/\n/g, '<br>')}</p>`;
            hasVitals = true; // Count the narrative as content
        }

        return hasVitals ? c : null;
    }, true);


    // 11. Labs / Diagnostic Studies
    addSection('Labs / Diagnostic Studies', () => {
        const dates = formDataObject['lab_date[]'] || [];
        const names = formDataObject['lab_name[]'] || [];
        const results = formDataObject['lab_result[]'] || [];
        if (!names.some(n => n.trim())) return null;

        let c = '';
        names.forEach((name, i) => {
            if (name.trim()) {
                const date = dates[i] || 'N/A';
                const result = results[i]?.trim() || 'No Result Recorded';
                c += `<div class="lab-entry"><p><strong>Date:</strong> ${date} | <strong>Test:</strong> ${name}</p><p><strong>Result:</strong> ${result.replace(/\n/g, '<br>')}</p></div>`;
            }
        });
        return c;
    });

    // 12. Assessment & Plan
    addSection('Assessment & Plan', () => {
        const diagnoses = formDataObject['ap_diagnosis[]'] || [];
        const mdms = formDataObject['ap_mdm[]'] || [];
        const plans = formDataObject['ap_plan[]'] || [];

        if (!diagnoses.some(d => d.trim())) return null;

        let c = '';
        diagnoses.forEach((diagnosis, i) => {
            if (diagnosis.trim()) {
                const mdm = mdms[i] || '';
                const plan = plans[i] || '';
                
                c += `<div style="margin-top: 20px; padding: 10px; border: 1px solid #ccc; border-radius: 5px;">`;
                c += `<h3>Diagnosis #${i + 1}: ${diagnosis}</h3>`;
                
                if (mdm.trim()) {
                    c += `<h4>Medical Decision-Making (MDM)</h4><p style="margin-left: 10px;">${mdm.trim().replace(/\n/g, '<br>')}</p>`;
                }
                
                if (plan.trim()) {
                    c += `<h4>Plan</h4><p style="margin-left: 10px;">${plan.trim().replace(/\n/g, '<br>')}</p>`;
                }
                c += `</div>`;
            }
        });
        return c;
    }, true);


    // 13. Signature & Attestation
    addSection('', () => {
        let c = '';
        const sigName = formDataObject['signature_name'];
        if (sigName?.trim()) {
          const now = new Date();
          c += `<p style="margin-top: 40px;">_________________________<br>${sigName}<br>Signed: ${now.toLocaleDateString()} ${now.toLocaleTimeString()}</p>`;
        }
        
        const attestation = formDataObject['academic_attestation'];
        if (attestation?.trim()) {
            c += `<h2>Academic Integrity Attestation</h2><p style="font-style: italic;">${attestation.replace(/\n/g, '<br>')}</p>`;
        }
        return c;
    }, true);


    htmlContent += `
        </body>
        </html>
    `;

    const blob = new Blob([htmlContent], { type: 'text/html' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `Clinical_Note_${formDataObject['patient_name'] ? formDataObject['patient_name'].replace(/[^a-zA-Z0-9]/g, '_') : 'Untitled'}_${formDataObject['encounter_date'] || new Date().toISOString().slice(0, 10)}.html`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
    
    // Clear local storage after successful export
    localStorage.removeItem(FORM_STORAGE_KEY);
    alert('Note exported successfully! All local data for this form has been cleared.');
}

</script>
</body>
</html>
