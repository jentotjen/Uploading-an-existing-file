<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบบริหารใบลาออก</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- เพิ่ม Library สำหรับแปลง HTML เป็น PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Sarabun', sans-serif;
            background-color: #f3f4f6; /* bg-gray-100 */
        }
        /* Custom scrollbar for better look */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1; 
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8; 
        }
        .fade-in {
            animation: fadeIn 0.3s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="text-gray-800 h-screen flex flex-col">

    <!-- Navbar -->
    <nav class="bg-blue-800 text-white shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <i class="fa-solid fa-file-signature text-2xl mr-3"></i>
                    <span class="font-bold text-xl tracking-wide">ResignEase System</span>
                </div>
                <div class="flex items-center space-x-4">
                    <div id="user-info" class="text-sm mr-4 hidden md:block opacity-80">
                        <!-- User info will be injected here -->
                    </div>
                    <button id="nav-employee" class="px-3 py-2 rounded-md text-sm font-medium bg-blue-900 hover:bg-blue-700 transition-colors" onclick="switchView('employee')">
                        <i class="fa-solid fa-user mr-1"></i> ยื่นคำร้อง
                    </button>
                    <!-- ปุ่มคณะกรรมการจะถูกซ่อนไว้เป็นค่าเริ่มต้น และแสดงเฉพาะผู้ที่มีสิทธิ์ -->
                    <button id="nav-hr" class="hidden px-3 py-2 rounded-md text-sm font-medium hover:bg-blue-700 transition-colors" onclick="switchView('hr')">
                        <i class="fa-solid fa-users-gear mr-1"></i> จัดการคำร้อง
                    </button>
                    <button onclick="logout()" class="px-3 py-2 rounded-md text-sm font-medium text-red-200 hover:bg-red-700 hover:text-white transition-colors ml-4 border border-red-400 border-opacity-30">
                        <i class="fa-solid fa-right-from-bracket mr-1"></i> ออกจากระบบ
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main Content Area -->
    <main class="flex-grow container mx-auto px-4 py-8 max-w-5xl overflow-y-auto">

        <!-- ================= EMPLOYEE VIEW ================= -->
        <div id="employee-view" class="fade-in block">
            <div class="bg-white rounded-xl shadow-lg overflow-hidden border border-gray-100">
                <div class="bg-blue-50 border-b border-blue-100 px-6 py-4">
                    <h2 class="text-2xl font-bold text-blue-800">
                        <i class="fa-solid fa-pen-to-square mr-2"></i> ยื่นแบบฟอร์มขอลาออก
                    </h2>
                    <p class="text-gray-600 text-sm mt-1">กรุณากรอกข้อมูลให้ครบถ้วนเพื่อดำเนินการตามขั้นตอนของชมรม/สมาคม</p>
                </div>
                
                <form id="resignation-form" class="p-6 space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <!-- Personal Info -->
                        <div class="space-y-4">
                            <div>
                                <label for="emp-id" class="block text-sm font-medium text-gray-700 mb-1">รหัสสมาชิก <span class="text-red-500">*</span></label>
                                <input type="text" id="emp-id" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-shadow outline-none" placeholder="เช่น MEM-00123">
                            </div>
                            <div>
                                <label for="emp-name" class="block text-sm font-medium text-gray-700 mb-1">ชื่อ-นามสกุล <span class="text-red-500">*</span></label>
                                <input type="text" id="emp-name" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-shadow outline-none" placeholder="นาย สมชาย ใจดี">
                            </div>
                            <div>
                                <label for="emp-department" class="block text-sm font-medium text-gray-700 mb-1">บทบาท / ฝ่าย <span class="text-red-500">*</span></label>
                                <select id="emp-department" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-shadow outline-none bg-white">
                                    <option value="" disabled selected>เลือกบทบาท...</option>
                                    <option value="สมาชิกทั่วไป">สมาชิกทั่วไป</option>
                                    <option value="ฝ่ายกิจกรรม">ฝ่ายกิจกรรม</option>
                                    <option value="ฝ่ายทะเบียน">ฝ่ายทะเบียน</option>
                                    <option value="ฝ่ายเหรัญญิก">ฝ่ายเหรัญญิก</option>
                                    <option value="คณะกรรมการ">คณะกรรมการบริหาร</option>
                                </select>
                            </div>
                        </div>

                        <!-- Resignation Details -->
                        <div class="space-y-4">
                            <div>
                                <label for="resign-date" class="block text-sm font-medium text-gray-700 mb-1">วันที่มีผลการลาออก <span class="text-red-500">*</span></label>
                                <input type="date" id="resign-date" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-shadow outline-none">
                                <p class="text-xs text-gray-500 mt-1">* ควรแจ้งล่วงหน้าอย่างน้อย 15 วันตามข้อบังคับ</p>
                            </div>
                            <div>
                                <label for="resign-reason" class="block text-sm font-medium text-gray-700 mb-1">เหตุผลในการลาออก <span class="text-red-500">*</span></label>
                                <select id="resign-reason" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-shadow outline-none bg-white">
                                    <option value="" disabled selected>เลือกเหตุผล...</option>
                                    <option value="ไม่มีเวลาเข้าร่วมกิจกรรม">ไม่มีเวลาเข้าร่วมกิจกรรม</option>
                                    <option value="ย้ายภูมิลำเนา">ย้ายภูมิลำเนา</option>
                                    <option value="ปัญหาสุขภาพ">ปัญหาสุขภาพ</option>
                                    <option value="ภาระหน้าที่การงาน/เรียน">ภาระหน้าที่การงาน/เรียน</option>
                                    <option value="เหตุผลส่วนตัว">เหตุผลส่วนตัว</option>
                                    <option value="อื่นๆ">อื่นๆ</option>
                                </select>
                            </div>
                            <div>
                                <label for="resign-note" class="block text-sm font-medium text-gray-700 mb-1">รายละเอียดเพิ่มเติม</label>
                                <textarea id="resign-note" rows="3" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-shadow outline-none resize-none" placeholder="อธิบายเพิ่มเติม (ถ้ามี)..."></textarea>
                            </div>
                        </div>
                    </div>
                    
                    <div class="pt-4 border-t border-gray-200 flex justify-end">
                        <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-6 rounded-lg shadow-md transition-all flex items-center">
                            <i class="fa-regular fa-paper-plane mr-2"></i> ยื่นใบลาออก
                        </button>
                    </div>
                </form>
            </div>

            <!-- Employee Status List -->
            <div class="mt-8 bg-white rounded-xl shadow-md overflow-hidden border border-gray-100">
                <div class="px-6 py-4 border-b border-gray-200 bg-gray-50 flex justify-between items-center">
                    <h3 class="text-lg font-bold text-gray-800"><i class="fa-solid fa-clock-rotate-left mr-2"></i> ประวัติการยื่นใบลาออกของคุณ</h3>
                </div>
                <div class="p-6">
                    <div id="employee-list-container" class="space-y-4">
                        <!-- Data will be injected here -->
                        <div class="text-center py-8 text-gray-500">
                            <i class="fa-solid fa-folder-open text-4xl mb-3 text-gray-300"></i>
                            <p>ยังไม่มีประวัติการยื่นใบลาออก</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- ================= HR/MANAGER VIEW ================= -->
        <div id="hr-view" class="fade-in hidden">
            
            <!-- Dashboard Stats -->
            <div class="grid grid-cols-1 md:grid-cols-4 gap-4 mb-6">
                <div class="bg-white rounded-xl shadow-sm p-4 border-l-4 border-blue-500 flex items-center justify-between">
                    <div>
                        <p class="text-sm text-gray-500 font-medium">ทั้งหมด</p>
                        <p class="text-2xl font-bold text-gray-800" id="stat-total">0</p>
                    </div>
                    <div class="p-3 bg-blue-100 rounded-full text-blue-600">
                        <i class="fa-solid fa-file-lines text-xl"></i>
                    </div>
                </div>
                <div class="bg-white rounded-xl shadow-sm p-4 border-l-4 border-yellow-400 flex items-center justify-between">
                    <div>
                        <p class="text-sm text-gray-500 font-medium">รออนุมัติ</p>
                        <p class="text-2xl font-bold text-gray-800" id="stat-pending">0</p>
                    </div>
                    <div class="p-3 bg-yellow-100 rounded-full text-yellow-600">
                        <i class="fa-solid fa-hourglass-half text-xl"></i>
                    </div>
                </div>
                <div class="bg-white rounded-xl shadow-sm p-4 border-l-4 border-green-500 flex items-center justify-between">
                    <div>
                        <p class="text-sm text-gray-500 font-medium">อนุมัติแล้ว</p>
                        <p class="text-2xl font-bold text-gray-800" id="stat-approved">0</p>
                    </div>
                    <div class="p-3 bg-green-100 rounded-full text-green-600">
                        <i class="fa-solid fa-check-circle text-xl"></i>
                    </div>
                </div>
                <div class="bg-white rounded-xl shadow-sm p-4 border-l-4 border-red-500 flex items-center justify-between">
                    <div>
                        <p class="text-sm text-gray-500 font-medium">ปฏิเสธ</p>
                        <p class="text-2xl font-bold text-gray-800" id="stat-rejected">0</p>
                    </div>
                    <div class="p-3 bg-red-100 rounded-full text-red-600">
                        <i class="fa-solid fa-times-circle text-xl"></i>
                    </div>
                </div>
            </div>

            <!-- Management Table -->
            <div class="bg-white rounded-xl shadow-lg overflow-hidden border border-gray-100">
                <div class="px-6 py-4 border-b border-gray-200 flex justify-between items-center bg-gray-50">
                    <h2 class="text-xl font-bold text-gray-800">
                        <i class="fa-solid fa-list-check mr-2"></i> รายการคำร้องขอลาออก
                    </h2>
                    <div class="flex space-x-2">
                        <select id="filter-status" class="px-3 py-1 border border-gray-300 rounded-md text-sm outline-none focus:border-blue-500" onchange="renderHRTable()">
                            <option value="all">สถานะทั้งหมด</option>
                            <option value="pending">รออนุมัติ</option>
                            <option value="approved">อนุมัติแล้ว</option>
                            <option value="rejected">ปฏิเสธ</option>
                        </select>
                    </div>
                </div>
                
                <div class="overflow-x-auto">
                    <table class="min-w-full divide-y divide-gray-200">
                        <thead class="bg-gray-50">
                            <tr>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">รหัสสมาชิก/ชื่อ</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">บทบาท</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">วันที่มีผล/เหตุผล</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">วันที่ยื่น</th>
                                <th scope="col" class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">สถานะ</th>
                                <th scope="col" class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">การจัดการ</th>
                            </tr>
                        </thead>
                        <tbody id="hr-table-body" class="bg-white divide-y divide-gray-200">
                            <!-- Data will be injected here -->
                            <tr>
                                <td colspan="6" class="px-6 py-12 text-center text-gray-500">
                                    <i class="fa-solid fa-inbox text-4xl mb-3 text-gray-300 block"></i>
                                    ไม่มีข้อมูลคำร้อง
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

    </main>

    <!-- Custom Modal for Alerts -->
    <div id="custom-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50 transition-opacity">
        <div class="bg-white rounded-xl shadow-2xl p-6 max-w-sm w-full mx-4 transform scale-95 transition-transform duration-200">
            <div id="modal-icon" class="text-center mb-4 text-3xl">
                <!-- Icon injected by JS -->
            </div>
            <h3 id="modal-title" class="text-lg font-bold text-center text-gray-800 mb-2">Title</h3>
            <p id="modal-message" class="text-gray-600 text-center mb-6 text-sm">Message here</p>
            <div class="flex justify-center">
                <button onclick="closeModal()" class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-6 rounded-lg shadow transition-colors w-full">
                    ตกลง
                </button>
            </div>
        </div>
    </div>

    <!-- Action Modal for HR (Approve/Reject) -->
    <div id="action-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50 transition-opacity">
        <div class="bg-white rounded-xl shadow-2xl p-6 max-w-md w-full mx-4">
            <h3 class="text-lg font-bold text-gray-800 mb-4" id="action-modal-title">ยืนยันการดำเนินการ</h3>
            
            <div class="mb-4 p-3 bg-gray-50 rounded border border-gray-200">
                <p class="text-sm text-gray-600">กำลังดำเนินการคำร้องของ: <span id="action-emp-name" class="font-bold text-gray-800"></span></p>
            </div>

            <div class="mb-4">
                <label for="action-comment" class="block text-sm font-medium text-gray-700 mb-1">ความคิดเห็น (จำเป็นสำหรับกรณีปฏิเสธ)</label>
                <textarea id="action-comment" rows="3" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none resize-none" placeholder="ระบุเหตุผล หรือข้อความถึงสมาชิก..."></textarea>
            </div>

            <input type="hidden" id="action-req-id">
            <input type="hidden" id="action-type">

            <div class="flex justify-end space-x-3">
                <button onclick="closeActionModal()" class="px-4 py-2 text-gray-600 bg-gray-100 hover:bg-gray-200 rounded-lg transition-colors font-medium">ยกเลิก</button>
                <button id="btn-confirm-action" onclick="confirmAction()" class="px-4 py-2 text-white font-medium rounded-lg transition-colors shadow">
                    ยืนยัน
                </button>
            </div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-4 right-4 bg-green-500 text-white px-6 py-3 rounded-lg shadow-lg transform translate-y-20 opacity-0 transition-all duration-300 z-50 flex items-center">
        <i class="fa-solid fa-circle-check mr-2"></i>
        <span id="toast-message">บันทึกสำเร็จ</span>
    </div>

    <!-- Line Notification Mock -->
    <div id="line-toast" class="fixed top-4 right-4 bg-[#00B900] text-white px-5 py-4 rounded-lg shadow-2xl transform translate-x-[150%] opacity-0 transition-all duration-500 z-[60] flex items-start max-w-sm border-l-4 border-green-800">
        <i class="fa-brands fa-line text-3xl mr-3 mt-1 text-white drop-shadow-md"></i>
        <div>
            <h4 class="font-bold text-sm mb-1 drop-shadow-sm">LINE Notify</h4>
            <p id="line-toast-message" class="text-sm leading-tight opacity-90 whitespace-pre-line"></p>
        </div>
    </div>

    <!-- Letter / PDF Modal -->
    <div id="letter-modal" class="fixed inset-0 bg-black bg-opacity-60 hidden flex items-center justify-center z-50 transition-opacity p-4">
        <div class="bg-white rounded-xl shadow-2xl max-w-4xl w-full flex flex-col max-h-[95vh] relative overflow-hidden">
            <!-- Loading Overlay for PDF generation -->
            <div id="pdf-loading" class="absolute inset-0 bg-white bg-opacity-80 z-20 hidden flex-col items-center justify-center">
                <i class="fa-solid fa-circle-notch fa-spin text-5xl text-blue-600 mb-4"></i>
                <p class="text-gray-800 font-bold text-lg">กำลังสร้างไฟล์ PDF...</p>
                <p class="text-gray-500 text-sm mt-1">กรุณารอสักครู่</p>
            </div>

            <div class="px-6 py-4 border-b border-gray-200 flex justify-between items-center bg-gray-50 rounded-t-xl z-10">
                <h3 class="text-lg font-bold text-gray-800"><i class="fa-solid fa-file-lines mr-2"></i> หนังสือขอลาออก (รูปแบบทางการ)</h3>
                <button onclick="closeLetterModal()" class="text-gray-400 hover:text-gray-700 transition-colors focus:outline-none">
                    <i class="fa-solid fa-times text-2xl"></i>
                </button>
            </div>
            
            <div class="p-4 sm:p-8 overflow-y-auto flex-grow bg-gray-300 flex justify-center custom-scrollbar">
                <!-- This content is what gets printed to PDF -->
                <div id="letter-content" class="bg-white text-black p-10 sm:p-14 font-sarabun mx-auto shadow-2xl relative" style="width: 210mm; max-width: 100%; min-height: 297mm; line-height: 1.8; box-sizing: border-box;">
                    
                    <!-- Watermark / Logo simulation -->
                    <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-gray-200 opacity-20 pointer-events-none z-0">
                        <i class="fa-solid fa-users" style="font-size: 20rem;"></i>
                    </div>

                    <div class="relative z-10 text-gray-900">
                        <!-- Header: Centered Logo and Title -->
                        <div class="text-center mb-8 flex flex-col items-center">
                            <label for="logo-upload" class="cursor-pointer group relative flex flex-col items-center justify-center mb-6">
                                <img id="letter-logo" src="https://placehold.co/120x120/1e3a8a/ffffff?text=LOGO" alt="Logo" class="w-28 h-28 object-cover rounded-full shadow-sm border-2 border-gray-200 group-hover:opacity-80 transition-opacity">
                                <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity bg-black bg-opacity-20 rounded-full">
                                    <i class="fa-solid fa-camera text-white text-2xl drop-shadow-md"></i>
                                </div>
                                <span data-html2canvas-ignore="true" class="text-xs text-blue-700 mt-3 font-medium bg-blue-50 hover:bg-blue-100 px-4 py-1.5 rounded-full shadow-sm transition-colors border border-blue-200 flex items-center">
                                    <i class="fa-solid fa-cloud-arrow-up mr-2"></i> อัปโหลดโลโก้ (ถ้ามี)
                                </span>
                            </label>
                            <input type="file" id="logo-upload" class="hidden" accept="image/*" onchange="previewLogo(event)">
                        </div>

                        <!-- Date (Aligned to right side, slightly indented) -->
                        <div class="flex justify-end mb-8 text-[15px]">
                            <div class="w-1/2 pl-4">
                                <div id="letter-date">เขียนที่ ระบบลงทะเบียนออนไลน์<br>วันที่ -</div>
                            </div>
                        </div>

                        <!-- Subject & Salutation -->
                        <div class="mb-3 text-[15px] font-bold">
                            <span class="inline-block w-14">เรื่อง</span> ขอลาออกจากการเป็นสมาชิกและพ้นจากตำแหน่งหน้าที่
                        </div>
                        <div class="mb-8 text-[15px] font-bold">
                            <span class="inline-block w-14">เรียน</span> คณะกรรมการบริหารและฝ่ายทะเบียน
                        </div>
                        
                        <!-- Body Paragraphs -->
                        <div class="indent-12 mb-4 text-[15px] text-justify leading-relaxed" id="letter-body-1">
                            ข้าพเจ้า (ชื่อ) รหัสสมาชิก (รหัส) ปัจจุบันดำรงตำแหน่ง (บทบาท) มีความประสงค์ขอลาออกจากการเป็นสมาชิกและพ้นจากตำแหน่งหน้าที่ของชมรม/สมาคม โดยให้มีผลตั้งแต่วันที่         (วันที่) เป็นต้นไป
                        </div>
                        <div class="indent-12 mb-4 text-[15px] text-justify leading-relaxed" id="letter-body-2">
                            สาเหตุของการลาออกในครั้งนี้ เนื่องจาก (เหตุผล) (หมายเหตุ)
                        </div>
                        <div class="indent-12 mb-16 text-[15px] text-justify leading-relaxed">
                            จึงเรียนมาเพื่อโปรดพิจารณาอนุมัติ และขอขอบพระคุณคณะกรรมการ ตลอดจนเพื่อนสมาชิกทุกท่าน ที่ได้ให้ความช่วยเหลือและสนับสนุนการปฏิบัติงานของข้าพเจ้าเป็นอย่างดีตลอดระยะเวลาที่ผ่านมา
                        </div>
                        
                        <!-- Signature Section -->
                        <div class="flex justify-end pr-8">
                            <div class="flex flex-col items-center w-64">
                                <div class="mb-14 text-center text-[15px]">ขอแสดงความนับถือ</div>
                                
                                <div class="w-full border-b border-dotted border-gray-600 mb-3"></div>
                                
                                <div id="letter-signature-name" class="font-bold mb-1 text-center text-[15px]">( - )</div>
                                <div id="letter-signature-position" class="text-center text-[14px]">ตำแหน่ง: -</div>
                            </div>
                        </div>

                        <!-- Status Stamp -->
                        <div id="letter-status-stamp" class="absolute bottom-4 left-4 border-4 px-6 py-2 rounded-lg text-xl font-bold transform -rotate-12 hidden opacity-70 tracking-widest pointer-events-none">
                            <!-- Status Stamp injected by JS -->
                        </div>
                    </div>
                </div>
            </div>

            <div class="px-6 py-4 border-t border-gray-200 bg-gray-50 flex justify-end space-x-3 rounded-b-xl z-10">
                <button onclick="copyLetterText()" class="px-4 py-2 text-gray-700 bg-white border border-gray-300 hover:bg-gray-50 rounded-lg transition-colors font-medium flex items-center shadow-sm">
                    <i class="fa-regular fa-copy mr-2"></i> คัดลอกข้อความ
                </button>
                <button onclick="downloadPDF()" class="px-4 py-2 text-white bg-red-600 hover:bg-red-700 rounded-lg transition-colors font-medium flex items-center shadow-sm">
                    <i class="fa-solid fa-file-pdf mr-2"></i> ดาวน์โหลด PDF
                </button>
            </div>
        </div>
    </div>

    <script>
        // --- Authentication & Authorization ---
        function checkAuth() {
            const role = sessionStorage.getItem('current_user_role');
            const name = sessionStorage.getItem('current_user_name');

            // ถ้าไม่มี role ถือว่ายังไม่ได้ล็อกอิน ให้กลับไปหน้า login
            if (!role) {
                window.location.href = 'login.html';
                return;
            }

            // แสดงชื่อผู้ใช้
            const userInfoEl = document.getElementById('user-info');
            if (userInfoEl) {
                userInfoEl.innerHTML = `<i class="fa-regular fa-circle-user mr-1"></i> ${name} (${role})`;
                userInfoEl.classList.remove('hidden');
            }

            // จัดการสิทธิ์การมองเห็น (Role-Based Access)
            const navHr = document.getElementById('nav-hr');
            if (role === 'admin' || role === 'officer') {
                navHr.classList.remove('hidden'); // แสดงปุ่มจัดการ
                // ถ้าเป็น admin/officer อาจจะอยากให้โผล่มาหน้าจัดการเลย
                // switchView('hr'); 
            } else {
                navHr.classList.add('hidden'); // ซ่อนปุ่มจัดการ
                // ล็อกให้แสดงแค่หน้ายื่นคำร้อง
                switchView('employee');
                
                // เติมชื่อลงในฟอร์มยื่นใบลาออกให้เลย (จำลองว่ามาจากฐานข้อมูล)
                document.getElementById('emp-name').value = name;
                document.getElementById('emp-name').readOnly = true; // ไม่ให้แก้ชื่อตัวเอง
                document.getElementById('emp-name').classList.add('bg-gray-100');
            }
        }

        function logout() {
            sessionStorage.removeItem('current_user_role');
            sessionStorage.removeItem('current_user_name');
            window.location.href = 'login.html';
        }

        // --- LINE OA / Webhook Notification System ---
        // นำ Webhook URL ของคุณมาใส่ที่นี่ (เช่น URL จาก Google Apps Script, Make.com, n8n หรือ API ของคุณ)
        // เพื่อรับข้อมูล JSON และส่งต่อไปยัง LINE Messaging API (LINE OA)
        const LINE_WEBHOOK_URL = 'https://script.google.com/macros/s/AKfycbz0zkkeRT15_-hDNxzzFovodYUzZllj11ul31FVN-yGADfSb1K1v8_jFOxLlfcZsUdEGw/exec'; 

        async function sendLineOANotification(actionType, data) {
            // 1. แสดงผลแจ้งเตือนจำลองบนหน้าจอ (UI Mockup)
            let mockMsg = '';
            if (actionType === 'new_request') {
                mockMsg = `🔔 มีคำร้องขอลาออกใหม่\nชื่อ: ${data.empName}\nฝ่าย: ${data.department}\n\nกรุณาตรวจสอบในระบบ (LINE OA)`;
            } else if (actionType === 'update_status') {
                const statusText = data.status === 'approved' ? '✅ อนุมัติ' : '❌ ปฏิเสธ';
                mockMsg = `📨 อัปเดตใบลาออก\nเรียน: ${data.empName}\nสถานะ: ${statusText}\nหมายเหตุ: ${data.hrComment || '-'}`;
            }
            simulateLineNotify(mockMsg);

            // 2. ส่งข้อมูลจริงไปยัง Webhook (ถ้ามีการตั้งค่า URL ไว้)
            if (LINE_WEBHOOK_URL) {
                try {
                    await fetch(LINE_WEBHOOK_URL, {
                        method: 'POST',
                        // ใช้ mode: 'no-cors' ถ้ายิงเข้า Google Apps Script โดยตรงเพื่อเลี่ยงปัญหา CORS
                        // แต่ถ้าเป็น API ของตัวเอง ให้เอา mode นี้ออก
                        mode: 'no-cors', 
                        headers: {
                            'Content-Type': 'application/json',
                        },
                        body: JSON.stringify({
                            action: actionType,
                            timestamp: new Date().toISOString(),
                            payload: data
                        })
                    });
                    console.log('ส่งข้อมูลไปยัง Webhook สำหรับ LINE OA สำเร็จ');
                } catch (error) {
                    console.error('ไม่สามารถส่งแจ้งเตือน LINE OA ได้:', error);
                }
            } else {
                console.log('จำลองการส่งข้อมูล LINE OA (ยังไม่ได้ตั้งค่า LINE_WEBHOOK_URL):', { action: actionType, payload: data });
            }
        }

        // State Management
        // In a real app, this would be a database. We use an array in memory.
        let resignRequests = [
            {
                id: 'REQ-1704067200000', // Mock timestamp
                empId: 'MEM-0042',
                empName: 'กฤติน ใจหวัง',
                department: 'สมาชิกทั่วไป',
                resignDate: '2027-01-31',
                reason: 'ภาระหน้าที่การงาน/เรียน',
                note: 'ปีนี้มีเรียนหนักมาก ไม่สามารถแบ่งเวลามาทำกิจกรรมได้ครับ',
                submitDate: '2026-10-01',
                status: 'pending',
                hrComment: ''
            },
            {
                id: 'REQ-1701388800000',
                empId: 'MEM-0015',
                empName: 'วิไลวรรณ สุขเกษม',
                department: 'ฝ่ายกิจกรรม',
                resignDate: '2026-12-31',
                reason: 'ย้ายภูมิลำเนา',
                note: 'ต้องย้ายกลับไปทำงานที่ต่างจังหวัดถาวร',
                submitDate: '2026-09-15',
                status: 'approved',
                hrComment: 'รับทราบครับ ขอให้โชคดีกับที่ทำงานใหม่ ว่างๆ แวะมาเยี่ยมชมรมได้เสมอครับ'
            }
        ];

        // Status configuration for UI mapping
        const statusConfig = {
            pending: { label: 'รออนุมัติ', color: 'bg-yellow-100 text-yellow-800 border-yellow-200', icon: 'fa-hourglass-half' },
            approved: { label: 'อนุมัติแล้ว', color: 'bg-green-100 text-green-800 border-green-200', icon: 'fa-check' },
            rejected: { label: 'ปฏิเสธ', color: 'bg-red-100 text-red-800 border-red-200', icon: 'fa-xmark' }
        };

        // Initialize application
        document.addEventListener('DOMContentLoaded', () => {
            // ตรวจสอบสิทธิ์ก่อนทำอย่างอื่น
            checkAuth();

            // Set minimum date for resignation to today
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('resign-date').setAttribute('min', today);
            
            // Set default date to 15 days from now to follow rules
            const defaultDate = new Date();
            defaultDate.setDate(defaultDate.getDate() + 15);
            document.getElementById('resign-date').value = defaultDate.toISOString().split('T')[0];

            // Render initial views
            renderEmployeeList();
            renderHRTable();
            updateStats();
        });

        // Navigation Logic
        function switchView(view) {
            const empView = document.getElementById('employee-view');
            const hrView = document.getElementById('hr-view');
            const navEmp = document.getElementById('nav-employee');
            const navHr = document.getElementById('nav-hr');

            if (view === 'employee') {
                empView.classList.remove('hidden');
                hrView.classList.add('hidden');
                navEmp.classList.add('bg-blue-900');
                navHr.classList.remove('bg-blue-900');
            } else {
                empView.classList.add('hidden');
                hrView.classList.remove('hidden');
                navHr.classList.add('bg-blue-900');
                navEmp.classList.remove('bg-blue-900');
                renderHRTable(); // Refresh table when entering HR view
                updateStats();
            }
        }

        // Form Submission Logic
        document.getElementById('resignation-form').addEventListener('submit', function(e) {
            e.preventDefault();

            // Gather data
            const empId = document.getElementById('emp-id').value.trim();
            const empName = document.getElementById('emp-name').value.trim();
            const department = document.getElementById('emp-department').value;
            const resignDate = document.getElementById('resign-date').value;
            const reason = document.getElementById('resign-reason').value;
            const note = document.getElementById('resign-note').value.trim();

            // Basic Validation (HTML5 covers most, this is extra check)
            if (!empId || !empName || !department || !resignDate || !reason) {
                showModal('ข้อผิดพลาด', 'กรุณากรอกข้อมูลที่จำเป็นให้ครบถ้วน', 'error');
                return;
            }

            // Check if date is at least 15 days away (Simulation of club rule)
            const submitDateObj = new Date();
            const resignDateObj = new Date(resignDate);
            const timeDiff = resignDateObj.getTime() - submitDateObj.getTime();
            const daysDiff = Math.ceil(timeDiff / (1000 * 3600 * 24));

            if (daysDiff < 15) {
                 showModal('แจ้งเตือน', 'การลาออกควรแจ้งล่วงหน้าอย่างน้อย 15 วันตามข้อบังคับชมรม เพื่อให้กรรมการรับทราบและจัดการงานต่อ', 'warning');
                 // We don't block submission, just warn
            }

            // Create new request object
            const newRequest = {
                id: 'REQ-' + Date.now(),
                empId: empId,
                empName: empName,
                department: department,
                resignDate: resignDate,
                reason: reason,
                note: note,
                submitDate: submitDateObj.toISOString().split('T')[0],
                status: 'pending',
                hrComment: ''
            };

            // Save to state
            resignRequests.unshift(newRequest); // Add to beginning

            // Reset form
            this.reset();
            // reset date to 15 days
            const dDate = new Date();
            dDate.setDate(dDate.getDate() + 15);
            document.getElementById('resign-date').value = dDate.toISOString().split('T')[0];

            // Update UI
            renderEmployeeList();
            updateStats();
            showToast('ยื่นแบบฟอร์มสำเร็จ ข้อมูลถูกส่งไปยังคณะกรรมการแล้ว');
            
            // เรียกใช้ฟังก์ชันส่งแจ้งเตือน LINE OA เมื่อมีการยื่นฟอร์มใหม่
            sendLineOANotification('new_request', newRequest);
        });

        // Render Employee's Own Requests (Simulation: Shows all requests for demo, usually filtered by logged in user)
        function renderEmployeeList() {
            const container = document.getElementById('employee-list-container');
            
            if (resignRequests.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-8 text-gray-500">
                        <i class="fa-solid fa-folder-open text-4xl mb-3 text-gray-300"></i>
                        <p>ยังไม่มีประวัติการยื่นใบลาออก</p>
                    </div>`;
                return;
            }

            let html = '';
            resignRequests.forEach(req => {
                const statusInfo = statusConfig[req.status];
                html += `
                    <div class="border border-gray-200 rounded-lg p-4 hover:shadow-md transition-shadow bg-white">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <h4 class="font-bold text-gray-800 text-lg">${req.id}</h4>
                                <p class="text-sm text-gray-600"><i class="fa-regular fa-calendar mr-1"></i> ยื่นเมื่อ: ${formatDate(req.submitDate)}</p>
                            </div>
                            <span class="px-3 py-1 rounded-full text-xs font-semibold border ${statusInfo.color} flex items-center">
                                <i class="fa-solid ${statusInfo.icon} mr-1"></i> ${statusInfo.label}
                            </span>
                        </div>
                        <div class="grid grid-cols-2 gap-2 mt-3 text-sm">
                            <div><span class="text-gray-500">วันที่มีผล:</span> <span class="font-medium text-gray-800">${formatDate(req.resignDate)}</span></div>
                            <div><span class="text-gray-500">เหตุผล:</span> <span class="font-medium text-gray-800">${req.reason}</span></div>
                        </div>
                        ${req.hrComment ? `
                        <div class="mt-3 p-3 bg-gray-50 rounded text-sm border-l-4 ${req.status === 'approved' ? 'border-green-400' : 'border-red-400'}">
                            <span class="font-semibold text-gray-700">ข้อความจากคณะกรรมการ:</span> ${req.hrComment}
                        </div>` : ''}
                        <div class="mt-4 pt-3 border-t border-gray-100 flex justify-end">
                            <button onclick="openLetterModal('${req.id}')" class="text-blue-600 hover:text-blue-800 text-sm font-medium flex items-center bg-blue-50 px-3 py-1.5 rounded-lg transition-colors">
                                <i class="fa-solid fa-file-pdf mr-1.5"></i> ดูใบลาออก / บันทึก PDF
                            </button>
                        </div>
                    </div>
                `;
            });
            container.innerHTML = html;
        }

        // Render HR Management Table
        function renderHRTable() {
            const tbody = document.getElementById('hr-table-body');
            const filterValue = document.getElementById('filter-status').value;
            
            const filteredRequests = filterValue === 'all' 
                ? resignRequests 
                : resignRequests.filter(req => req.status === filterValue);

            if (filteredRequests.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="6" class="px-6 py-12 text-center text-gray-500">
                            <i class="fa-solid fa-inbox text-4xl mb-3 text-gray-300 block"></i>
                            ไม่พบข้อมูลคำร้องตามเงื่อนไขที่เลือก
                        </td>
                    </tr>`;
                return;
            }

            let html = '';
            filteredRequests.forEach(req => {
                const statusInfo = statusConfig[req.status];
                html += `
                    <tr class="hover:bg-gray-50 transition-colors">
                        <td class="px-6 py-4 whitespace-nowrap">
                            <div class="flex items-center">
                                <div class="flex-shrink-0 h-10 w-10 bg-blue-100 rounded-full flex items-center justify-center text-blue-600 font-bold">
                                    ${req.empName.charAt(0)}
                                </div>
                                <div class="ml-4">
                                    <div class="text-sm font-medium text-gray-900">${req.empName}</div>
                                    <div class="text-sm text-gray-500">${req.empId}</div>
                                </div>
                            </div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="px-2 py-1 inline-flex text-xs leading-5 font-semibold rounded-md bg-gray-100 text-gray-800">
                                ${req.department}
                            </span>
                        </td>
                        <td class="px-6 py-4">
                            <div class="text-sm text-gray-900 font-medium">${formatDate(req.resignDate)}</div>
                            <div class="text-sm text-gray-500 truncate max-w-xs" title="${req.note}">${req.reason}</div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                            ${formatDate(req.submitDate)}
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-center">
                            <span class="px-3 py-1 inline-flex text-xs leading-5 font-semibold rounded-full border ${statusInfo.color}">
                                ${statusInfo.label}
                            </span>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-center text-sm font-medium">
                            ${req.status === 'pending' ? `
                                <button onclick="openActionModal('${req.id}', 'approve')" class="text-green-600 hover:text-green-900 bg-green-50 hover:bg-green-100 px-3 py-1 rounded-md transition-colors mr-1 border border-green-200" title="อนุมัติ">
                                    <i class="fa-solid fa-check"></i>
                                </button>
                                <button onclick="openActionModal('${req.id}', 'reject')" class="text-red-600 hover:text-red-900 bg-red-50 hover:bg-red-100 px-3 py-1 rounded-md transition-colors mr-1 border border-red-200" title="ปฏิเสธ">
                                    <i class="fa-solid fa-xmark"></i>
                                </button>
                            ` : ''}
                            <button onclick="openLetterModal('${req.id}')" class="text-blue-600 hover:text-blue-900 bg-blue-50 hover:bg-blue-100 px-3 py-1 rounded-md transition-colors border border-blue-200" title="ดูใบลาออก / PDF">
                                <i class="fa-solid fa-file-pdf"></i>
                            </button>
                        </td>
                    </tr>
                `;
            });
            tbody.innerHTML = html;
        }

        // Update Dashboard Statistics
        function updateStats() {
            const total = resignRequests.length;
            const pending = resignRequests.filter(r => r.status === 'pending').length;
            const approved = resignRequests.filter(r => r.status === 'approved').length;
            const rejected = resignRequests.filter(r => r.status === 'rejected').length;

            // Animate numbers (simple version)
            document.getElementById('stat-total').innerText = total;
            document.getElementById('stat-pending').innerText = pending;
            document.getElementById('stat-approved').innerText = approved;
            document.getElementById('stat-rejected').innerText = rejected;
        }

        // Action Modal Handling (Approve/Reject)
        function openActionModal(id, actionType) {
            const request = resignRequests.find(r => r.id === id);
            if (!request) return;

            document.getElementById('action-req-id').value = id;
            document.getElementById('action-type').value = actionType;
            document.getElementById('action-emp-name').innerText = `${request.empName} (${request.empId})`;
            
            const titleEl = document.getElementById('action-modal-title');
            const btnConfirm = document.getElementById('btn-confirm-action');
            const commentBox = document.getElementById('action-comment');
            
            commentBox.value = ''; // Reset

            if (actionType === 'approve') {
                titleEl.innerText = 'ยืนยันการรับทราบ/อนุมัติการลาออก';
                titleEl.className = 'text-lg font-bold text-green-700 mb-4';
                btnConfirm.className = 'px-4 py-2 text-white font-medium rounded-lg transition-colors shadow bg-green-600 hover:bg-green-700';
                commentBox.placeholder = 'ข้อความอวยพรหรือหมายเหตุถึงสมาชิก (เลือกกรอกได้)...';
            } else {
                titleEl.innerText = 'ยืนยันการปฏิเสธ/ระงับใบลาออก';
                titleEl.className = 'text-lg font-bold text-red-700 mb-4';
                btnConfirm.className = 'px-4 py-2 text-white font-medium rounded-lg transition-colors shadow bg-red-600 hover:bg-red-700';
                commentBox.placeholder = 'โปรดระบุเหตุผลที่ปฏิเสธ (จำเป็น)...';
            }

            document.getElementById('action-modal').classList.remove('hidden');
        }

        function closeActionModal() {
            document.getElementById('action-modal').classList.add('hidden');
        }

        function confirmAction() {
            const id = document.getElementById('action-req-id').value;
            const actionType = document.getElementById('action-type').value;
            const comment = document.getElementById('action-comment').value.trim();

            if (actionType === 'reject' && !comment) {
                showModal('ข้อผิดพลาด', 'กรุณาระบุเหตุผลในการปฏิเสธคำร้อง', 'error');
                return;
            }

            const requestIndex = resignRequests.findIndex(r => r.id === id);
            if (requestIndex !== -1) {
                const req = resignRequests[requestIndex];
                req.status = actionType === 'approve' ? 'approved' : 'rejected';
                req.hrComment = comment;
                
                closeActionModal();
                renderHRTable();
                updateStats();
                renderEmployeeList(); // Update employee view silently
                
                showToast(actionType === 'approve' ? 'อนุมัติคำร้องเรียบร้อยแล้ว' : 'ปฏิเสธคำร้องเรียบร้อยแล้ว');
                
                // เรียกใช้ฟังก์ชันส่งแจ้งเตือน LINE OA เมื่อมีการอัปเดตสถานะ
                sendLineOANotification('update_status', req);
            }
        }

        function showDetails(id) {
            const request = resignRequests.find(r => r.id === id);
            if (request) {
                const msg = `สมาชิก: ${request.empName}\nบทบาท: ${request.department}\nเหตุผล: ${request.reason}\n\nข้อความจากคณะกรรมการ: ${request.hrComment || '-'}`;
                showModal(`รายละเอียดคำร้อง ${id}`, msg, 'info');
            }
        }

        // Utility: Custom Modal Alert
        function showModal(title, message, type = 'info') {
            const modal = document.getElementById('custom-modal');
            const titleEl = document.getElementById('modal-title');
            const msgEl = document.getElementById('modal-message');
            const iconEl = document.getElementById('modal-icon');

            titleEl.innerText = title;
            msgEl.innerText = message;

            let iconHtml = '';
            if (type === 'error') {
                iconHtml = '<i class="fa-solid fa-circle-xmark text-red-500"></i>';
                titleEl.className = 'text-lg font-bold text-center text-red-600 mb-2';
            } else if (type === 'warning') {
                iconHtml = '<i class="fa-solid fa-triangle-exclamation text-yellow-500"></i>';
                titleEl.className = 'text-lg font-bold text-center text-yellow-600 mb-2';
            } else {
                iconHtml = '<i class="fa-solid fa-circle-info text-blue-500"></i>';
                titleEl.className = 'text-lg font-bold text-center text-blue-600 mb-2';
            }
            iconEl.innerHTML = iconHtml;

            modal.classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('custom-modal').classList.add('hidden');
        }

        // Utility: Toast Notification
        function showToast(message) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-message').innerText = message;
            
            toast.classList.remove('translate-y-20', 'opacity-0');
            
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        function simulateLineNotify(message) {
            const toast = document.getElementById('line-toast');
            document.getElementById('line-toast-message').innerText = message;
            
            // Show toast
            toast.classList.remove('translate-x-[150%]', 'opacity-0');
            
            // Hide after 5 seconds
            setTimeout(() => {
                toast.classList.add('translate-x-[150%]', 'opacity-0');
            }, 5000);
        }

        // Preview Logo Upload
        function previewLogo(event) {
            const input = event.target;
            if (input.files && input.files[0]) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    document.getElementById('letter-logo').src = e.target.result;
                };
                reader.readAsDataURL(input.files[0]);
            }
        }

        let currentLetterReqId = null;

        function openLetterModal(id) {
            const req = resignRequests.find(r => r.id === id);
            if (!req) return;
            
            currentLetterReqId = id;

            // Render Date using Thai format
            const submitDateObj = new Date(req.submitDate);
            const thaiMonths = ["มกราคม", "กุมภาพันธ์", "มีนาคม", "เมษายน", "พฤษภาคม", "มิถุนายน", "กรกฎาคม", "สิงหาคม", "กันยายน", "ตุลาคม", "พฤศจิกายน", "ธันวาคม"];
            const formattedSubmitDate = `${submitDateObj.getDate()} ${thaiMonths[submitDateObj.getMonth()]} ${submitDateObj.getFullYear() + 543}`;
            
            const resignDateObj = new Date(req.resignDate);
            const formattedResignDate = `${resignDateObj.getDate()} ${thaiMonths[resignDateObj.getMonth()]} ${resignDateObj.getFullYear() + 543}`;

            // Populate Letter Elements
            document.getElementById('letter-date').innerHTML = `เขียนที่ ระบบลงทะเบียนออนไลน์<br>วันที่ ${formattedSubmitDate}`;
            
            // ขัดเกลาข้อความให้เป็นทางการและสละสลวยขึ้น
            document.getElementById('letter-body-1').innerText = `ข้าพเจ้า ${req.empName} รหัสสมาชิก ${req.empId} ปัจจุบันดำรงตำแหน่ง ${req.department} มีความประสงค์ขอลาออกจากการเป็นสมาชิกและพ้นจากตำแหน่งหน้าที่ของชมรม/สมาคม โดยให้มีผลตั้งแต่วันที่ ${formattedResignDate} เป็นต้นไป`;
            
            const noteText = req.note ? ` ทั้งนี้เนื่องจาก ${req.note}` : '';
            document.getElementById('letter-body-2').innerText = `สาเหตุของการลาออกในครั้งนี้ เนื่องจาก ${req.reason}${noteText}`;
            
            document.getElementById('letter-signature-name').innerText = `( ${req.empName} )`;
            document.getElementById('letter-signature-position').innerText = `ตำแหน่ง: ${req.department}`;

            // Handle Status Stamp (Watermark on letter)
            const stamp = document.getElementById('letter-status-stamp');
            stamp.classList.remove('hidden', 'text-green-600', 'border-green-600', 'text-red-600', 'border-red-600', 'text-yellow-600', 'border-yellow-600');
            
            if (req.status === 'approved') {
                stamp.innerText = 'อนุมัติแล้ว (APPROVED)';
                stamp.classList.add('text-green-600', 'border-green-600');
            } else if (req.status === 'rejected') {
                stamp.innerText = 'ปฏิเสธ (REJECTED)';
                stamp.classList.add('text-red-600', 'border-red-600');
            } else {
                stamp.innerText = 'รอพิจารณา (PENDING)';
                stamp.classList.add('text-yellow-600', 'border-yellow-600');
            }

            document.getElementById('letter-modal').classList.remove('hidden');
        }

        function closeLetterModal() {
            document.getElementById('letter-modal').classList.add('hidden');
            currentLetterReqId = null;
        }

        function copyLetterText() {
            const req = resignRequests.find(r => r.id === currentLetterReqId);
            if (!req) return;

            const dateInfo = document.getElementById('letter-date').innerText;
            const b1 = document.getElementById('letter-body-1').innerText;
            const b2 = document.getElementById('letter-body-2').innerText;
            
            // ปรับ Template ข้อความคัดลอกให้สวยงาม
            const plainText = `${dateInfo}

เรื่อง ขอลาออกจากการเป็นสมาชิกและพ้นจากตำแหน่งหน้าที่
เรียน คณะกรรมการบริหารและฝ่ายทะเบียน

        ${b1}

        ${b2}

        จึงเรียนมาเพื่อโปรดพิจารณาอนุมัติ และขอขอบพระคุณคณะกรรมการ ตลอดจนเพื่อนสมาชิกทุกท่าน ที่ได้ให้ความช่วยเหลือและสนับสนุนการปฏิบัติงานของข้าพเจ้าเป็นอย่างดีตลอดระยะเวลาที่ผ่านมา

ขอแสดงความนับถือ

( ${req.empName} )
ตำแหน่ง: ${req.department}`;

            navigator.clipboard.writeText(plainText).then(() => {
                showToast('คัดลอกข้อความใบลาออกเรียบร้อยแล้ว');
            }).catch(err => {
                console.error('Failed to copy: ', err);
                showModal('เกิดข้อผิดพลาด', 'ไม่สามารถคัดลอกข้อความได้ กรุณาลองใหม่อีกครั้ง', 'error');
            });
        }

        function downloadPDF() {
            const req = resignRequests.find(r => r.id === currentLetterReqId);
            if (!req) return;

            const element = document.getElementById('letter-content');
            const loadingOverlay = document.getElementById('pdf-loading');
            
            loadingOverlay.classList.remove('hidden');
            loadingOverlay.classList.add('flex');

            // Configure PDF options
            const opt = {
                margin:       [10, 10, 10, 10], // top, left, bottom, right
                filename:     `ใบลาออก_${req.empName.replace(/\s+/g, '_')}_${req.empId}.pdf`,
                image:        { type: 'jpeg', quality: 0.98 },
                html2canvas:  { scale: 2, useCORS: true, logging: false },
                jsPDF:        { unit: 'mm', format: 'a4', orientation: 'portrait' }
            };

            // Generate PDF
            html2pdf().set(opt).from(element).save().then(() => {
                loadingOverlay.classList.add('hidden');
                loadingOverlay.classList.remove('flex');
                showToast('ดาวน์โหลด PDF สำเร็จ');
            }).catch(err => {
                loadingOverlay.classList.add('hidden');
                loadingOverlay.classList.remove('flex');
                console.error('PDF Generation Error:', err);
                showModal('เกิดข้อผิดพลาด', 'ไม่สามารถสร้างไฟล์ PDF ได้', 'error');
            });
        }

        // Utility: Format Date (YYYY-MM-DD to DD/MM/YYYY)
        function formatDate(dateString) {
            if (!dateString) return '-';
            const [year, month, day] = dateString.split('-');
            return `${day}/${month}/${year}`;
        }
    </script>
</body>
</html>
