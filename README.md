# Axaprojectresource
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Resource Management Tool</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }
        .fade-in { animation: fadeIn 0.3s ease-in; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .resource-card { transition: all 0.2s ease; }
        .resource-card:hover { transform: translateY(-2px); box-shadow: 0 8px 25px rgba(0,0,0,0.1); }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-100 min-h-screen">
    <div class="container mx-auto px-4 py-8 max-w-7xl">
        <!-- Header -->
        <div class="text-center mb-8">
            <h1 class="text-4xl font-bold text-gray-800 mb-2">Resource Management</h1>
            <p class="text-gray-600">Track, organize, and manage your resources efficiently</p>
        </div>

        <!-- Dashboard Tab Content -->
        <div id="dashboardContent">
            <!-- Stats Dashboard -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                <div class="bg-white rounded-xl p-6 shadow-lg">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-sm font-medium text-gray-600">Total Resources</p>
                            <p class="text-2xl font-bold text-gray-900" id="totalCount">0</p>
                        </div>
                        <div class="bg-blue-100 p-3 rounded-full">
                            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"></path>
                            </svg>
                        </div>
                    </div>
                </div>
                <div class="bg-white rounded-xl p-6 shadow-lg">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-sm font-medium text-gray-600">Total Available Hrs</p>
                            <p class="text-2xl font-bold text-green-600" id="availableHours">0</p>
                        </div>
                        <div class="bg-green-100 p-3 rounded-full">
                            <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                        </div>
                    </div>
                </div>
                <div class="bg-white rounded-xl p-6 shadow-lg">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-sm font-medium text-gray-600">Allocated Hrs</p>
                            <p class="text-2xl font-bold text-orange-600" id="allocatedHours">0</p>
                        </div>
                        <div class="bg-orange-100 p-3 rounded-full">
                            <svg class="w-6 h-6 text-orange-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v10a2 2 0 002 2h8a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4"></path>
                            </svg>
                        </div>
                    </div>
                </div>
                <div class="bg-white rounded-xl p-6 shadow-lg">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-sm font-medium text-gray-600">Productivity Hrs</p>
                            <p class="text-2xl font-bold text-purple-600" id="productivityHours">0</p>
                        </div>
                        <div class="bg-purple-100 p-3 rounded-full">
                            <svg class="w-6 h-6 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"></path>
                            </svg>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Dashboard View Toggle -->
            <div class="bg-white rounded-xl p-6 shadow-lg mb-8">
                <div class="flex items-center justify-between mb-6">
                    <h3 class="text-xl font-semibold text-gray-800">Data Overview</h3>
                    <div class="flex gap-2">
                        <button onclick="switchDashboardView('resource')" id="resourceViewBtn" class="px-4 py-2 bg-blue-600 text-white rounded-lg font-medium transition-colors">
                            Resource View
                        </button>
                        <button onclick="switchDashboardView('project')" id="projectViewBtn" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-lg font-medium transition-colors hover:bg-gray-300">
                            Project View
                        </button>
                    </div>
                </div>

                <!-- Resource Table View -->
                <div id="resourceTableView">
                    <div class="overflow-x-auto">
                        <table class="w-full">
                            <thead>
                                <tr class="border-b border-gray-200">
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Name</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Category</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Worker Type</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Project</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Role</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Available Hrs</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Allocated Hrs</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Actual Hrs</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Productivity %</th>
                                </tr>
                            </thead>
                            <tbody id="resourceTableBody">
                                <!-- Resource rows will be populated here -->
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Project Table View -->
                <div id="projectTableView" class="hidden">
                    <div class="overflow-x-auto">
                        <table class="w-full">
                            <thead>
                                <tr class="border-b border-gray-200">
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Project Name</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Status</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Priority</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Start Date</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">End Date</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Assigned Resources</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Total Allocated Hrs</th>
                                    <th class="text-left py-3 px-4 font-semibold text-gray-700">Total Actual Hrs</th>
                                </tr>
                            </thead>
                            <tbody id="projectTableBody">
                                <!-- Project rows will be populated here -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- Tab Navigation -->
        <div class="bg-white rounded-xl shadow-lg mb-8">
            <div class="flex border-b border-gray-200">
                <button onclick="switchTab('dashboard')" id="dashboardTab" class="flex-1 px-6 py-4 text-center font-medium transition-colors bg-blue-600 text-white rounded-tl-xl">
                    Dashboard
                </button>
                <button onclick="switchTab('resources')" id="resourcesTab" class="flex-1 px-6 py-4 text-center font-medium transition-colors text-gray-600 hover:text-gray-800">
                    Resources
                </button>
                <button onclick="switchTab('projects')" id="projectsTab" class="flex-1 px-6 py-4 text-center font-medium transition-colors text-gray-600 hover:text-gray-800 rounded-tr-xl">
                    Projects
                </button>
            </div>
        </div>

        <!-- Resources Tab Content -->
        <div id="resourcesContent" class="hidden">
            <!-- Controls -->
            <div class="bg-white rounded-xl p-6 shadow-lg mb-8">
                <div class="flex flex-col lg:flex-row gap-4 items-center justify-between">
                    <div class="flex flex-col sm:flex-row gap-4 w-full lg:w-auto">
                        <button onclick="openAddModal()" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-lg font-medium transition-colors flex items-center gap-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path>
                            </svg>
                            Add Resource
                        </button>
                    <select id="categoryFilter" onchange="filterResources()" class="px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                        <option value="">All Categories</option>
                        <option value="Change Managers">Change Managers</option>
                        <option value="Learning Management">Learning Management</option>
                        <option value="Process Management">Process Management</option>
                    </select>

                    <select id="workerTypeFilter" onchange="filterResources()" class="px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                        <option value="">All Worker Types</option>
                        <option value="FTE">FTE</option>
                        <option value="PBH">PBH</option>
                    </select>

                </div>
                <div class="flex gap-4 w-full lg:w-auto">
                    <input type="text" id="searchInput" placeholder="Search resources..." onkeyup="filterResources()" class="flex-1 lg:w-64 px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
            </div>
        </div>

        <!-- Resources Grid -->
        <div id="resourcesGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <!-- Resources will be populated here -->
        </div>

        <!-- Empty State -->
        <div id="emptyState" class="text-center py-16 hidden">
            <svg class="w-24 h-24 text-gray-300 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"></path>
            </svg>
            <h3 class="text-xl font-medium text-gray-500 mb-2">No resources found</h3>
            <p class="text-gray-400 mb-6">Get started by adding your first resource</p>
            <button onclick="openAddModal()" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-lg font-medium transition-colors">
                Add Resource
            </button>
        </div>
        </div>

        <!-- Projects Tab Content -->
        <div id="projectsContent" class="hidden">
            <!-- Project Controls -->
            <div class="bg-white rounded-xl p-6 shadow-lg mb-8">
                <div class="flex flex-col lg:flex-row gap-4 items-center justify-between">
                    <div class="flex flex-col sm:flex-row gap-4 w-full lg:w-auto">
                        <button onclick="openAddProjectModal()" class="bg-green-600 hover:bg-green-700 text-white px-6 py-3 rounded-lg font-medium transition-colors flex items-center gap-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path>
                            </svg>
                            Add Project
                        </button>
                        <select id="projectStatusFilter" onchange="filterProjects()" class="px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            <option value="">All Statuses</option>
                            <option value="On Track">On Track</option>
                            <option value="Off Track">Off Track</option>
                            <option value="At Risk">At Risk</option>
                            <option value="Cancelled">Cancelled</option>
                            <option value="On Hold">On Hold</option>
                            <option value="Completed">Completed</option>
                        </select>
                    </div>
                    <div class="flex gap-4 w-full lg:w-auto">
                        <input type="text" id="projectSearchInput" placeholder="Search projects..." onkeyup="filterProjects()" class="flex-1 lg:w-64 px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    </div>
                </div>
            </div>

            <!-- Projects Grid -->
            <div id="projectsGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Projects will be populated here -->
            </div>

            <!-- Projects Empty State -->
            <div id="projectsEmptyState" class="text-center py-16 hidden">
                <svg class="w-24 h-24 text-gray-300 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"></path>
                </svg>
                <h3 class="text-xl font-medium text-gray-500 mb-2">No projects found</h3>
                <p class="text-gray-400 mb-6">Get started by adding your first project</p>
                <button onclick="openAddProjectModal()" class="bg-green-600 hover:bg-green-700 text-white px-6 py-3 rounded-lg font-medium transition-colors">
                    Add Project
                </button>
            </div>
        </div>
    </div>

    <!-- Add/Edit Modal -->
    <div id="resourceModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50 p-4">
        <div class="bg-white rounded-xl max-w-md w-full max-h-[90vh] overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-6">
                    <h2 id="modalTitle" class="text-2xl font-bold text-gray-800">Add Resource</h2>
                    <button onclick="closeModal()" class="text-gray-400 hover:text-gray-600 transition-colors">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                        </svg>
                    </button>
                </div>
                
                <form id="resourceForm" onsubmit="saveResource(event)">
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Resource Name</label>
                            <input type="text" id="resourceName" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Category</label>
                            <select id="resourceCategory" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                <option value="">Select Category</option>
                                <option value="Change Managers">Change Managers</option>
                                <option value="Learning Management">Learning Management</option>
                                <option value="Process Management">Process Management</option>
                            </select>
                        </div>
                        

                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Worker Type</label>
                            <select id="resourceWorkerType" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                <option value="">Select Worker Type</option>
                                <option value="FTE">FTE</option>
                                <option value="PBH">PBH</option>
                            </select>
                        </div>
                        


                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Project</label>
                            <select id="resourceProject" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                <option value="">Select Project</option>
                            </select>
                        </div>

                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Role</label>
                            <input type="text" id="resourceRole" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter role in project">
                        </div>

                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Estimated Effort (%)</label>
                                <input type="number" id="resourceEffortAllocation" min="0" max="100" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="0-100">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Actual Hrs Worked</label>
                                <input type="number" id="resourceActualHours" min="0" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="0">
                            </div>
                        </div>

                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Notes</label>
                            <textarea id="resourceNotes" rows="3" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"></textarea>
                        </div>
                    </div>
                    
                    <div class="flex gap-3 mt-6">
                        <button type="submit" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white py-3 rounded-lg font-medium transition-colors">
                            Save Resource
                        </button>
                        <button type="button" onclick="closeModal()" class="px-6 py-3 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition-colors">
                            Cancel
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Add/Edit Project Modal -->
    <div id="projectModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50 p-4">
        <div class="bg-white rounded-xl max-w-md w-full max-h-[90vh] overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-6">
                    <h2 id="projectModalTitle" class="text-2xl font-bold text-gray-800">Add Project</h2>
                    <button onclick="closeProjectModal()" class="text-gray-400 hover:text-gray-600 transition-colors">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                        </svg>
                    </button>
                </div>
                
                <form id="projectForm" onsubmit="saveProject(event)">
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Project Name</label>
                            <input type="text" id="projectName" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Description</label>
                            <textarea id="projectDescription" rows="3" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Project description"></textarea>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Status</label>
                            <select id="projectStatus" required class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                <option value="">Select Status</option>
                                <option value="On Track">On Track</option>
                                <option value="Off Track">Off Track</option>
                                <option value="At Risk">At Risk</option>
                                <option value="Cancelled">Cancelled</option>
                                <option value="On Hold">On Hold</option>
                                <option value="Completed">Completed</option>
                            </select>
                        </div>

                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Start Date</label>
                                <input type="date" id="projectStartDate" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">End Date</label>
                                <input type="date" id="projectEndDate" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                            </div>
                        </div>

                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Priority</label>
                            <select id="projectPriority" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                <option value="">Select Priority</option>
                                <option value="Low">Low</option>
                                <option value="Medium">Medium</option>
                                <option value="High">High</option>
                                <option value="Critical">Critical</option>
                            </select>
                        </div>


                    </div>
                    
                    <div class="flex gap-3 mt-6">
                        <button type="submit" class="flex-1 bg-green-600 hover:bg-green-700 text-white py-3 rounded-lg font-medium transition-colors">
                            Save Project
                        </button>
                        <button type="button" onclick="closeProjectModal()" class="px-6 py-3 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition-colors">
                            Cancel
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <script>
        let resources = [];
        let projects = [];
        let editingId = null;
        let editingProjectId = null;
        let currentTab = 'dashboard';
        let dashboardView = 'resource';

        // Initialize with empty data
        resources = [];
        projects = [];

        // Tab switching
        function switchTab(tab) {
            currentTab = tab;
            
            // Update tab buttons
            document.getElementById('dashboardTab').className = tab === 'dashboard' 
                ? 'flex-1 px-6 py-4 text-center font-medium transition-colors bg-blue-600 text-white rounded-tl-xl'
                : 'flex-1 px-6 py-4 text-center font-medium transition-colors text-gray-600 hover:text-gray-800 rounded-tl-xl';
            
            document.getElementById('resourcesTab').className = tab === 'resources' 
                ? 'flex-1 px-6 py-4 text-center font-medium transition-colors bg-blue-600 text-white'
                : 'flex-1 px-6 py-4 text-center font-medium transition-colors text-gray-600 hover:text-gray-800';
            
            document.getElementById('projectsTab').className = tab === 'projects' 
                ? 'flex-1 px-6 py-4 text-center font-medium transition-colors bg-blue-600 text-white rounded-tr-xl'
                : 'flex-1 px-6 py-4 text-center font-medium transition-colors text-gray-600 hover:text-gray-800 rounded-tr-xl';
            
            // Show/hide content
            document.getElementById('dashboardContent').style.display = tab === 'dashboard' ? 'block' : 'none';
            document.getElementById('resourcesContent').style.display = tab === 'resources' ? 'block' : 'none';
            document.getElementById('projectsContent').style.display = tab === 'projects' ? 'block' : 'none';
            
            if (tab === 'dashboard') {
                renderDashboard();
            } else if (tab === 'projects') {
                renderProjects();
            } else if (tab === 'resources') {
                renderResources();
            }
        }

        // Dashboard view switching
        function switchDashboardView(view) {
            dashboardView = view;
            
            // Update view buttons
            document.getElementById('resourceViewBtn').className = view === 'resource'
                ? 'px-4 py-2 bg-blue-600 text-white rounded-lg font-medium transition-colors'
                : 'px-4 py-2 bg-gray-200 text-gray-700 rounded-lg font-medium transition-colors hover:bg-gray-300';
            
            document.getElementById('projectViewBtn').className = view === 'project'
                ? 'px-4 py-2 bg-blue-600 text-white rounded-lg font-medium transition-colors'
                : 'px-4 py-2 bg-gray-200 text-gray-700 rounded-lg font-medium transition-colors hover:bg-gray-300';
            
            // Show/hide table views
            document.getElementById('resourceTableView').style.display = view === 'resource' ? 'block' : 'none';
            document.getElementById('projectTableView').style.display = view === 'project' ? 'block' : 'none';
            
            renderDashboard();
        }

        // Project Management Functions
        function openAddProjectModal() {
            editingProjectId = null;
            document.getElementById('projectModalTitle').textContent = 'Add Project';
            document.getElementById('projectForm').reset();
            document.getElementById('projectModal').classList.remove('hidden');
            document.getElementById('projectModal').classList.add('flex');
        }

        function openEditProjectModal(id) {
            const project = projects.find(p => p.id === id);
            if (!project) return;

            editingProjectId = id;
            document.getElementById('projectModalTitle').textContent = 'Edit Project';
            document.getElementById('projectName').value = project.name;
            document.getElementById('projectDescription').value = project.description || '';
            document.getElementById('projectStatus').value = project.status;
            document.getElementById('projectStartDate').value = project.startDate || '';
            document.getElementById('projectEndDate').value = project.endDate || '';
            document.getElementById('projectPriority').value = project.priority || '';

            
            document.getElementById('projectModal').classList.remove('hidden');
            document.getElementById('projectModal').classList.add('flex');
        }

        function closeProjectModal() {
            document.getElementById('projectModal').classList.add('hidden');
            document.getElementById('projectModal').classList.remove('flex');
        }

        function saveProject(event) {
            event.preventDefault();
            
            const formData = {
                name: document.getElementById('projectName').value,
                description: document.getElementById('projectDescription').value,
                status: document.getElementById('projectStatus').value,
                startDate: document.getElementById('projectStartDate').value,
                endDate: document.getElementById('projectEndDate').value,
                priority: document.getElementById('projectPriority').value,

            };

            if (editingProjectId) {
                const index = projects.findIndex(p => p.id === editingProjectId);
                projects[index] = { ...projects[index], ...formData };
            } else {
                const newProject = {
                    id: Date.now(),
                    ...formData,
                    dateCreated: new Date().toISOString()
                };
                projects.push(newProject);
            }

            closeProjectModal();
            renderProjects();
            updateProjectDropdown();
            if (currentTab === 'dashboard') {
                renderDashboard();
            }
        }

        function deleteProject(id) {
            if (confirm('Are you sure you want to delete this project? This will also remove it from any assigned resources.')) {
                projects = projects.filter(p => p.id !== id);
                
                // Remove project from resources
                resources.forEach(resource => {
                    if (resource.project === projects.find(p => p.id === id)?.name) {
                        resource.project = '';
                        resource.role = '';
                        resource.effortAllocation = 0;
                        resource.actualHours = 0;
                    }
                });
                
                renderProjects();
                updateProjectDropdown();
                if (currentTab === 'resources') {
                    renderResources();
                    updateStats();
                }
                if (currentTab === 'dashboard') {
                    renderDashboard();
                }
            }
        }

        function updateProjectDropdown() {
            const dropdown = document.getElementById('resourceProject');
            dropdown.innerHTML = '<option value="">Select Project</option>';
            
            projects.forEach(project => {
                const option = document.createElement('option');
                option.value = project.name;
                option.textContent = project.name;
                dropdown.appendChild(option);
            });
        }

        function openAddModal() {
            editingId = null;
            document.getElementById('modalTitle').textContent = 'Add Resource';
            document.getElementById('resourceForm').reset();
            document.getElementById('resourceModal').classList.remove('hidden');
            document.getElementById('resourceModal').classList.add('flex');
        }

        function openEditModal(id) {
            const resource = resources.find(r => r.id === id);
            if (!resource) return;

            editingId = id;
            document.getElementById('modalTitle').textContent = 'Edit Resource';
            document.getElementById('resourceName').value = resource.name;
            document.getElementById('resourceCategory').value = resource.category;
            document.getElementById('resourceWorkerType').value = resource.workerType || '';

            document.getElementById('resourceProject').value = resource.project || '';
            document.getElementById('resourceRole').value = resource.role || '';
            document.getElementById('resourceEffortAllocation').value = resource.effortAllocation || '';
            document.getElementById('resourceActualHours').value = resource.actualHours || '';
            document.getElementById('resourceNotes').value = resource.notes || '';
            
            document.getElementById('resourceModal').classList.remove('hidden');
            document.getElementById('resourceModal').classList.add('flex');
        }

        function closeModal() {
            document.getElementById('resourceModal').classList.add('hidden');
            document.getElementById('resourceModal').classList.remove('flex');
        }

        function saveResource(event) {
            event.preventDefault();
            
            const formData = {
                name: document.getElementById('resourceName').value,
                category: document.getElementById('resourceCategory').value,
                workerType: document.getElementById('resourceWorkerType').value,

                project: document.getElementById('resourceProject').value,
                role: document.getElementById('resourceRole').value,
                effortAllocation: parseInt(document.getElementById('resourceEffortAllocation').value) || 0,
                actualHours: parseInt(document.getElementById('resourceActualHours').value) || 0,
                notes: document.getElementById('resourceNotes').value
            };

            if (editingId) {
                const index = resources.findIndex(r => r.id === editingId);
                resources[index] = { ...resources[index], ...formData };
            } else {
                const newResource = {
                    id: Date.now(),
                    ...formData,
                    dateAdded: new Date().toISOString()
                };
                resources.push(newResource);
            }

            closeModal();
            renderResources();
            updateStats();
            if (currentTab === 'dashboard') {
                renderDashboard();
            }
        }

        function deleteResource(id) {
            if (confirm('Are you sure you want to delete this resource?')) {
                resources = resources.filter(r => r.id !== id);
                renderResources();
                updateStats();
                if (currentTab === 'dashboard') {
                    renderDashboard();
                }
            }
        }



        function getCategoryIcon(category) {
            const icons = {
                'Change Managers': '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4"></path></svg>',
                'Learning Management': '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"></path></svg>',
                'Process Management': '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v10a2 2 0 002 2h8a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01"></path></svg>'
            };
            return icons[category] || '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10"></path></svg>';
        }

        function renderResources() {
            const grid = document.getElementById('resourcesGrid');
            const emptyState = document.getElementById('emptyState');
            
            const filteredResources = getFilteredResources();
            
            if (filteredResources.length === 0) {
                grid.innerHTML = '';
                emptyState.classList.remove('hidden');
                return;
            }
            
            emptyState.classList.add('hidden');
            
            grid.innerHTML = filteredResources.map(resource => {
                return `
                    <div class="resource-card bg-white rounded-xl p-6 shadow-lg fade-in">
                        <div class="flex items-start justify-between mb-4">
                            <div class="flex items-center gap-3">
                                <div class="text-gray-600">
                                    ${getCategoryIcon(resource.category)}
                                </div>
                                <div>
                                    <h3 class="font-semibold text-gray-800 text-lg">${resource.name}</h3>
                                    <p class="text-sm text-gray-500">${resource.category}</p>
                                </div>
                            </div>
                            <div class="flex gap-2">
                                <button onclick="openEditModal(${resource.id})" class="text-gray-400 hover:text-blue-600 transition-colors">
                                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path>
                                    </svg>
                                </button>
                                <button onclick="deleteResource(${resource.id})" class="text-gray-400 hover:text-red-600 transition-colors">
                                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path>
                                    </svg>
                                </button>
                            </div>
                        </div>
                        
                        <div class="space-y-3">
                            ${resource.workerType ? `
                                <div class="flex items-center justify-between">
                                    <span class="text-sm text-gray-600">Worker Type:</span>
                                    <span class="px-3 py-1 rounded-full text-xs font-medium ${resource.workerType === 'FTE' ? 'bg-green-100 text-green-800' : 'bg-orange-100 text-orange-800'}">${resource.workerType}</span>
                                </div>
                            ` : ''}
                            


                            ${resource.project ? `
                                <div class="flex items-center justify-between">
                                    <span class="text-sm text-gray-600">Project:</span>
                                    <span class="text-sm font-medium text-gray-800">${resource.project}</span>
                                </div>
                            ` : ''}

                            ${resource.role ? `
                                <div class="flex items-center justify-between">
                                    <span class="text-sm text-gray-600">Role:</span>
                                    <span class="text-sm text-gray-600">${resource.role}</span>
                                </div>
                            ` : ''}

                            <div class="grid grid-cols-2 gap-4 pt-2">
                                <div class="text-center">
                                    <p class="text-xs text-gray-500">Available Hrs</p>
                                    <p class="text-lg font-semibold text-green-600">${160 - Math.round((resource.effortAllocation || 0) * 160 / 100)}</p>
                                </div>
                                <div class="text-center">
                                    <p class="text-xs text-gray-500">Allocated</p>
                                    <p class="text-lg font-semibold text-orange-600">${Math.round((resource.effortAllocation || 0) * 160 / 100)}h (${resource.effortAllocation || 0}%)</p>
                                </div>
                            </div>

                            ${resource.actualHours > 0 ? `
                                <div class="pt-2 border-t border-gray-100">
                                    <div class="flex items-center justify-between">
                                        <span class="text-sm text-gray-600">Actual Hours:</span>
                                        <span class="text-sm font-medium text-purple-600">${resource.actualHours}h</span>
                                    </div>
                                    <div class="flex items-center justify-between">
                                        <span class="text-sm text-gray-600">Productivity:</span>
                                        <span class="text-sm font-medium text-purple-600">${Math.round((resource.actualHours / Math.max(1, Math.round((resource.effortAllocation || 0) * 160 / 100))) * 100)}%</span>
                                    </div>
                                </div>
                            ` : ''}
                            
                            ${resource.notes ? `
                                <div class="mt-3 pt-3 border-t border-gray-100">
                                    <p class="text-sm text-gray-600">${resource.notes}</p>
                                </div>
                            ` : ''}
                        </div>
                    </div>
                `;
            }).join('');
        }

        function getFilteredResources() {
            const categoryFilter = document.getElementById('categoryFilter').value;
            const workerTypeFilter = document.getElementById('workerTypeFilter').value;
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            
            return resources.filter(resource => {
                const matchesCategory = !categoryFilter || resource.category === categoryFilter;
                const matchesWorkerType = !workerTypeFilter || resource.workerType === workerTypeFilter;
                const matchesSearch = !searchTerm || 
                    resource.name.toLowerCase().includes(searchTerm) ||
                    resource.category.toLowerCase().includes(searchTerm) ||
                    resource.workerType?.toLowerCase().includes(searchTerm) ||

                    resource.project?.toLowerCase().includes(searchTerm) ||
                    resource.role?.toLowerCase().includes(searchTerm) ||
                    resource.notes?.toLowerCase().includes(searchTerm);
                
                return matchesCategory && matchesWorkerType && matchesSearch;
            });
        }

        function filterResources() {
            renderResources();
        }

        function updateStats() {
            const total = resources.length;
            const totalAvailableHours = total * 160;
            const totalAllocatedHours = resources.reduce((sum, r) => sum + Math.round((r.effortAllocation || 0) * 160 / 100), 0);
            const totalProductivityHours = resources.reduce((sum, r) => sum + (r.actualHours || 0), 0);
            
            document.getElementById('totalCount').textContent = total;
            document.getElementById('availableHours').textContent = totalAvailableHours - totalAllocatedHours;
            document.getElementById('allocatedHours').textContent = totalAllocatedHours;
            document.getElementById('productivityHours').textContent = totalProductivityHours;
        }

        // Close modal when clicking outside
        document.getElementById('resourceModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeModal();
            }
        });

        function renderProjects() {
            const grid = document.getElementById('projectsGrid');
            const emptyState = document.getElementById('projectsEmptyState');
            
            const filteredProjects = getFilteredProjects();
            
            if (filteredProjects.length === 0) {
                grid.innerHTML = '';
                emptyState.classList.remove('hidden');
                return;
            }
            
            emptyState.classList.add('hidden');
            
            grid.innerHTML = filteredProjects.map(project => {
                const statusColors = {
                    'On Track': 'bg-green-100 text-green-800',
                    'Off Track': 'bg-red-100 text-red-800',
                    'At Risk': 'bg-yellow-100 text-yellow-800',
                    'Cancelled': 'bg-gray-100 text-gray-800',
                    'On Hold': 'bg-orange-100 text-orange-800',
                    'Completed': 'bg-blue-100 text-blue-800'
                };

                const priorityColors = {
                    'Low': 'bg-gray-100 text-gray-800',
                    'Medium': 'bg-blue-100 text-blue-800',
                    'High': 'bg-orange-100 text-orange-800',
                    'Critical': 'bg-red-100 text-red-800'
                };

                const assignedResources = resources.filter(r => r.project === project.name);
                
                return `
                    <div class="resource-card bg-white rounded-xl p-6 shadow-lg fade-in">
                        <div class="flex items-start justify-between mb-4">
                            <div>
                                <h3 class="font-semibold text-gray-800 text-lg mb-2">${project.name}</h3>
                                <div class="flex gap-2 mb-2">
                                    <span class="px-3 py-1 rounded-full text-xs font-medium ${statusColors[project.status] || 'bg-gray-100 text-gray-800'}">${project.status}</span>
                                    ${project.priority ? `<span class="px-3 py-1 rounded-full text-xs font-medium ${priorityColors[project.priority] || 'bg-gray-100 text-gray-800'}">${project.priority}</span>` : ''}
                                </div>
                            </div>
                            <div class="flex gap-2">
                                <button onclick="openEditProjectModal(${project.id})" class="text-gray-400 hover:text-blue-600 transition-colors">
                                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path>
                                    </svg>
                                </button>
                                <button onclick="deleteProject(${project.id})" class="text-gray-400 hover:text-red-600 transition-colors">
                                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path>
                                    </svg>
                                </button>
                            </div>
                        </div>
                        
                        <div class="space-y-3">
                            ${project.description ? `
                                <p class="text-sm text-gray-600">${project.description}</p>
                            ` : ''}
                            
                            ${project.startDate || project.endDate ? `
                                <div class="flex items-center justify-between text-sm">
                                    ${project.startDate ? `<span class="text-gray-600">Start: ${new Date(project.startDate).toLocaleDateString()}</span>` : '<span></span>'}
                                    ${project.endDate ? `<span class="text-gray-600">End: ${new Date(project.endDate).toLocaleDateString()}</span>` : '<span></span>'}
                                </div>
                            ` : ''}
                            

                            
                            <div class="pt-3 border-t border-gray-100">
                                <div class="flex items-center justify-between">
                                    <span class="text-sm text-gray-600">Assigned Resources:</span>
                                    <span class="text-sm font-medium text-blue-600">${assignedResources.length}</span>
                                </div>
                                ${assignedResources.length > 0 ? `
                                    <div class="mt-2">
                                        ${assignedResources.slice(0, 3).map(r => `<span class="inline-block bg-blue-100 text-blue-800 text-xs px-2 py-1 rounded mr-1 mb-1">${r.name}</span>`).join('')}
                                        ${assignedResources.length > 3 ? `<span class="text-xs text-gray-500">+${assignedResources.length - 3} more</span>` : ''}
                                    </div>
                                ` : ''}
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function getFilteredProjects() {
            const statusFilter = document.getElementById('projectStatusFilter').value;
            const searchTerm = document.getElementById('projectSearchInput').value.toLowerCase();
            
            return projects.filter(project => {
                const matchesStatus = !statusFilter || project.status === statusFilter;
                const matchesSearch = !searchTerm || 
                    project.name.toLowerCase().includes(searchTerm) ||
                    project.description?.toLowerCase().includes(searchTerm) ||
                    project.status.toLowerCase().includes(searchTerm) ||
                    project.priority?.toLowerCase().includes(searchTerm);
                
                return matchesStatus && matchesSearch;
            });
        }

        function filterProjects() {
            renderProjects();
        }

        // Close project modal when clicking outside
        document.getElementById('projectModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeProjectModal();
            }
        });

        // Dashboard rendering functions
        function renderDashboard() {
            updateStats();
            if (dashboardView === 'resource') {
                renderResourceTable();
            } else {
                renderProjectTable();
            }
        }

        function renderResourceTable() {
            const tbody = document.getElementById('resourceTableBody');
            
            if (resources.length === 0) {
                tbody.innerHTML = '<tr><td colspan="9" class="text-center py-8 text-gray-500">No resources available</td></tr>';
                return;
            }
            
            tbody.innerHTML = resources.map(resource => {
                const availableHours = 160 - Math.round((resource.effortAllocation || 0) * 160 / 100);
                const allocatedHours = Math.round((resource.effortAllocation || 0) * 160 / 100);
                const actualHours = resource.actualHours || 0;
                const productivity = allocatedHours > 0 ? Math.round((actualHours / allocatedHours) * 100) : 0;
                
                return `
                    <tr class="border-b border-gray-100 hover:bg-gray-50">
                        <td class="py-3 px-4 font-medium text-gray-900">${resource.name}</td>
                        <td class="py-3 px-4 text-gray-600">${resource.category}</td>
                        <td class="py-3 px-4">
                            ${resource.workerType ? `<span class="px-2 py-1 rounded-full text-xs font-medium ${resource.workerType === 'FTE' ? 'bg-green-100 text-green-800' : 'bg-orange-100 text-orange-800'}">${resource.workerType}</span>` : '-'}
                        </td>
                        <td class="py-3 px-4 text-gray-600">${resource.project || '-'}</td>
                        <td class="py-3 px-4 text-gray-600">${resource.role || '-'}</td>
                        <td class="py-3 px-4 text-green-600 font-semibold">${availableHours}h</td>
                        <td class="py-3 px-4 text-orange-600 font-semibold">${allocatedHours}h (${resource.effortAllocation || 0}%)</td>
                        <td class="py-3 px-4 text-purple-600 font-semibold">${actualHours}h</td>
                        <td class="py-3 px-4 text-purple-600 font-semibold">${productivity}%</td>
                    </tr>
                `;
            }).join('');
        }

        function renderProjectTable() {
            const tbody = document.getElementById('projectTableBody');
            
            if (projects.length === 0) {
                tbody.innerHTML = '<tr><td colspan="8" class="text-center py-8 text-gray-500">No projects available</td></tr>';
                return;
            }
            
            tbody.innerHTML = projects.map(project => {
                const assignedResources = resources.filter(r => r.project === project.name);
                const totalAllocatedHours = assignedResources.reduce((sum, r) => sum + Math.round((r.effortAllocation || 0) * 160 / 100), 0);
                const totalActualHours = assignedResources.reduce((sum, r) => sum + (r.actualHours || 0), 0);
                
                const statusColors = {
                    'On Track': 'bg-green-100 text-green-800',
                    'Off Track': 'bg-red-100 text-red-800',
                    'At Risk': 'bg-yellow-100 text-yellow-800',
                    'Cancelled': 'bg-gray-100 text-gray-800',
                    'On Hold': 'bg-orange-100 text-orange-800',
                    'Completed': 'bg-blue-100 text-blue-800'
                };

                const priorityColors = {
                    'Low': 'bg-gray-100 text-gray-800',
                    'Medium': 'bg-blue-100 text-blue-800',
                    'High': 'bg-orange-100 text-orange-800',
                    'Critical': 'bg-red-100 text-red-800'
                };
                
                return `
                    <tr class="border-b border-gray-100 hover:bg-gray-50">
                        <td class="py-3 px-4 font-medium text-gray-900">${project.name}</td>
                        <td class="py-3 px-4">
                            <span class="px-2 py-1 rounded-full text-xs font-medium ${statusColors[project.status] || 'bg-gray-100 text-gray-800'}">${project.status}</span>
                        </td>
                        <td class="py-3 px-4">
                            ${project.priority ? `<span class="px-2 py-1 rounded-full text-xs font-medium ${priorityColors[project.priority] || 'bg-gray-100 text-gray-800'}">${project.priority}</span>` : '-'}
                        </td>
                        <td class="py-3 px-4 text-gray-600">${project.startDate ? new Date(project.startDate).toLocaleDateString() : '-'}</td>
                        <td class="py-3 px-4 text-gray-600">${project.endDate ? new Date(project.endDate).toLocaleDateString() : '-'}</td>
                        <td class="py-3 px-4 text-blue-600 font-semibold">${assignedResources.length}</td>
                        <td class="py-3 px-4 text-orange-600 font-semibold">${totalAllocatedHours}h</td>
                        <td class="py-3 px-4 text-purple-600 font-semibold">${totalActualHours}h</td>
                    </tr>
                `;
            }).join('');
        }

        // Initialize
        renderDashboard();
        updateProjectDropdown();
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9806dada932b03e9',t:'MTc1ODA5Mzc3Mi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
