<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>هوشیار</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;500;600;700&display=swap');
        * {
            font-family: 'Vazirmatn', sans-serif;
        }
        .gradient-bg {
            background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
        }
        .profile-circle {
            background: linear-gradient(90deg, #000 50%, #ffd700 50%);
        }
        .gold-accent {
            background: linear-gradient(135deg, #ffd700 0%, #ffed4e 100%);
        }
        .black-card {
            background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
        }
        .pulse-animation {
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        .slide-in {
            animation: slideIn 0.3s ease-out;
        }
        @keyframes slideIn {
            from { transform: translateY(-20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        @keyframes loadingBar {
            0% { width: 0%; }
            50% { width: 70%; }
            100% { width: 100%; }
        }
    </style>
</head>
<body class="gradient-bg min-h-screen">
    <!-- صفحه اولیه لودینگ -->
    <div id="initialLoading" class="min-h-screen flex items-center justify-center p-4">
        <div class="text-center">
            <div class="w-16 h-16 mx-auto mb-4 border-4 border-yellow-400 border-t-transparent rounded-full animate-spin"></div>
            <h1 class="text-2xl font-bold text-yellow-400 mb-2">هوشیار</h1>
            <p class="text-gray-300">در حال بارگذاری...</p>
        </div>
    </div>
    <!-- صفحه ثبت نام -->
    <div id="registerPage" class="hidden min-h-screen flex items-center justify-center p-4">
        <div class="black-card rounded-2xl shadow-2xl p-8 w-full max-w-md slide-in border border-yellow-500">
            <div class="text-center mb-8">
                <h1 class="text-3xl font-bold text-yellow-400 mb-2">
                    <svg class="w-10 h-10 inline-block mr-2" viewBox="0 0 24 24" fill="currentColor">
                        <path d="M20,5H4C2.89,5 2,5.89 2,7V17C2,18.11 2.89,19 4,19H20C21.11,19 22,18.11 22,17V7C22,5.89 21.11,5 20,5M20,17H4V7H20V17M9.5,8A1.5,1.5 0 0,0 8,9.5A1.5,1.5 0 0,0 9.5,11A1.5,1.5 0 0,0 11,9.5A1.5,1.5 0 0,0 9.5,8M14.5,13A1.5,1.5 0 0,0 13,14.5A1.5,1.5 0 0,0 14.5,16A1.5,1.5 0 0,0 16,14.5A1.5,1.5 0 0,0 14.5,13Z"/>
                    </svg>
                    هوشیار
                </h1>
                <p class="text-gray-300">به بازی هوشیار خوش آمدید</p>
            </div>
            
            <div class="space-y-6">
                <div>
                    <label class="block text-sm font-medium text-yellow-400 mb-2">نام کاربری</label>
                    <input type="text" id="username" class="w-full px-4 py-3 bg-gray-800 border border-yellow-500 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent text-white" placeholder="نام کاربری خود را وارد کنید">
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-yellow-400 mb-2">سن</label>
                    <input type="number" id="age" class="w-full px-4 py-3 bg-gray-800 border border-yellow-500 rounded-lg focus:ring-2 focus:ring-yellow-400 focus:border-transparent text-white" placeholder="سن خود را وارد کنید">
                </div>
                
                <div class="flex items-center">
                    <input type="checkbox" id="terms" class="h-4 w-4 text-yellow-500 focus:ring-yellow-400 border-yellow-500 rounded bg-gray-800">
                    <label for="terms" class="mr-2 block text-sm text-gray-300">
                        تمامی قوانین را می‌پذیرم
                    </label>
                </div>
                
                <button onclick="register()" class="w-full gold-accent hover:bg-yellow-600 text-black font-bold py-3 px-4 rounded-lg transition duration-200">
                    ثبت نام
                </button>
            </div>
        </div>
    </div>

    <!-- منوی اصلی -->
    <div id="mainMenu" class="hidden min-h-screen p-4">
        <!-- هدر -->
        <div class="flex justify-between items-center mb-8">
            <!-- پروفایل -->
            <div class="black-card rounded-xl p-4 shadow-lg flex items-center space-x-4 space-x-reverse border border-yellow-500">
                <div class="profile-circle w-12 h-12 rounded-full"></div>
                <div class="flex-1">
                    <div class="flex items-center space-x-2 space-x-reverse">
                        <div class="font-bold text-yellow-400" id="playerName">کاربر</div>
                        <button onclick="editName()" class="text-gray-400 hover:text-yellow-400 transition duration-200">
                            <svg class="w-4 h-4" viewBox="0 0 24 24" fill="currentColor">
                                <path d="M20.71,7.04C21.1,6.65 21.1,6 20.71,5.63L18.37,3.29C18,2.9 17.35,2.9 16.96,3.29L15.12,5.12L18.87,8.87M3,17.25V21H6.75L17.81,9.93L14.06,6.18L3,17.25Z"/>
                            </svg>
                        </button>
                    </div>
                    <div class="text-sm text-gray-300">
                        <svg class="w-4 h-4 inline-block ml-1" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M5,16L3,5H1V3H4L6,14H18.5L20.5,7H8V5H22L19.5,16H5Z"/>
                        </svg>
                        <span id="playerCups">0</span> کاپ
                    </div>
                </div>
            </div>
            
            <!-- تنظیمات -->
            <button onclick="showSettings()" class="black-card p-3 rounded-xl shadow-lg hover:shadow-xl transition duration-200 border border-yellow-500">
                <svg class="w-6 h-6 text-yellow-400" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12,15.5A3.5,3.5 0 0,1 8.5,12A3.5,3.5 0 0,1 12,8.5A3.5,3.5 0 0,1 15.5,12A3.5,3.5 0 0,1 12,15.5M19.43,12.97C19.47,12.65 19.5,12.33 19.5,12C19.5,11.67 19.47,11.34 19.43,11L21.54,9.37C21.73,9.22 21.78,8.95 21.66,8.73L19.66,5.27C19.54,5.05 19.27,4.96 19.05,5.05L16.56,6.05C16.04,5.66 15.5,5.32 14.87,5.07L14.5,2.42C14.46,2.18 14.25,2 14,2H10C9.75,2 9.54,2.18 9.5,2.42L9.13,5.07C8.5,5.32 7.96,5.66 7.44,6.05L4.95,5.05C4.73,4.96 4.46,5.05 4.34,5.27L2.34,8.73C2.22,8.95 2.27,9.22 2.46,9.37L4.57,11C4.53,11.34 4.5,11.67 4.5,12C4.5,12.33 4.53,12.65 4.57,12.97L2.46,14.63C2.27,14.78 2.22,15.05 2.34,15.27L4.34,18.73C4.46,18.95 4.73,19.03 4.95,18.95L7.44,17.94C7.96,18.34 8.5,18.68 9.13,18.93L9.5,21.58C9.54,21.82 9.75,22 10,22H14C14.25,22 14.46,21.82 14.5,21.58L14.87,18.93C15.5,18.68 16.04,18.34 16.56,17.94L19.05,18.95C19.27,19.03 19.54,18.95 19.66,18.73L21.66,15.27C21.78,15.05 21.73,14.78 21.54,14.63L19.43,12.97Z"/>
                </svg>
            </button>
        </div>

        <!-- دکمه‌های اصلی -->
        <div class="flex flex-col items-center justify-center min-h-[60vh] space-y-3">
            <button onclick="startOnlineGame()" class="gold-accent hover:bg-yellow-600 text-black font-medium py-3 px-6 rounded-lg text-base shadow-lg hover:shadow-xl transition duration-300 w-48">
                <svg class="w-5 h-5 inline-block ml-2" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M17,3A2,2 0 0,1 19,5V15A2,2 0 0,1 17,17H13V19H14A1,1 0 0,1 15,20H22V22H15A1,1 0 0,1 14,23H10A1,1 0 0,1 9,22H2V20H9A1,1 0 0,1 10,19H11V17H7C5.89,17 5,16.1 5,15V5A2,2 0 0,1 7,3H17M17,5H7V15H17V5Z"/>
                </svg>
                بازی آنلاین
            </button>
            <button onclick="showLevels()" class="black-card hover:bg-gray-700 text-yellow-400 font-medium py-3 px-6 rounded-lg text-base shadow-lg hover:shadow-xl transition duration-300 w-48 border border-yellow-500">
                <svg class="w-5 h-5 inline-block ml-2" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M7.5,4A5.5,5.5 0 0,0 2,9.5C2,10 2.09,10.5 2.22,11H6.3L7.57,7.63C7.87,6.83 9.05,6.75 9.43,7.63L11.5,13L12.09,11.58C12.22,11.25 12.57,11 13,11H21.78C21.91,10.5 22,10 22,9.5A5.5,5.5 0 0,0 16.5,4C14.64,4 13.04,4.92 12,6.34C10.96,4.92 9.36,4 7.5,4M3,12.5A1,1 0 0,0 2,13.5A1,1 0 0,0 3,14.5H5.44L11,20C12,20.9 12,20.9 13,20L18.56,14.5H21A1,1 0 0,0 22,13.5A1,1 0 0,0 21,12.5H13.4L12.47,14.8C12.07,15.81 10.92,15.67 10.55,14.83L8.5,9.5L7.54,11.83C7.39,12.21 7.05,12.5 6.6,12.5H3Z"/>
                </svg>
                شروع بازی
            </button>
        </div>

        <!-- پیام خطای اینترنت -->
        <div id="internetError" class="hidden fixed top-4 left-4 right-4 z-50">
            <div class="black-card rounded-xl p-4 mx-auto max-w-md border border-red-500 bg-red-900 bg-opacity-20">
                <div class="flex items-center space-x-3 space-x-reverse">
                    <svg class="w-6 h-6 text-red-400 flex-shrink-0" viewBox="0 0 24 24" fill="currentColor">
                        <path d="M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2M12,17A1.5,1.5 0 0,1 10.5,15.5A1.5,1.5 0 0,1 12,14A1.5,1.5 0 0,1 13.5,15.5A1.5,1.5 0 0,1 12,17M12,10A1,1 0 0,1 13,11V14A1,1 0 0,1 11,14V11A1,1 0 0,1 12,10Z"/>
                    </svg>
                    <div class="flex-1">
                        <div class="font-bold text-red-400 text-sm">خطای اتصال اینترنت</div>
                        <div class="text-red-300 text-xs">برای ورود به بازی حتماً اینترنت خود را روشن کنید</div>
                    </div>
                    <button onclick="hideInternetError()" class="text-red-400 hover:text-red-300">
                        <svg class="w-5 h-5" viewBox="0 0 24 24" fill="currentColor">
                            <path d="M19,6.41L17.59,5L12,10.59L6.41,5L5,6.41L10.59,12L5,17.59L6.41,19L12,13.41L17.59,19L19,17.59L13.41,12L19,6.41Z"/>
                        </svg>
                    </button>
                </div>
            </div>
        </div>

        <!-- دکمه‌های پایین -->
        <div class="fixed bottom-4 left-4 right-4 flex justify-center space-x-4 space-x-reverse">
            <button class="black-card p-3 rounded-xl shadow-lg hover:shadow-xl transition duration-200 flex-1 max-w-24 border border-yellow-500 text-yellow-400">
                <svg class="w-6 h-6 mx-auto mb-1" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M19,7H18V6A2,2 0 0,0 16,4H8A2,2 0 0,0 6,6V7H5A1,1 0 0,0 4,8V19A3,3 0 0,0 7,22H17A3,3 0 0,0 20,19V8A1,1 0 0,0 19,7M8,6H16V7H8V6M18,19A1,1 0 0,1 17,20H7A1,1 0 0,1 6,19V9H18V19Z"/>
                </svg>
                <span class="text-xs">فروشگاه</span>
            </button>
            <button class="black-card p-3 rounded-xl shadow-lg hover:shadow-xl transition duration-200 flex-1 max-w-24 border border-yellow-500 text-yellow-400">
                <svg class="w-6 h-6 mx-auto mb-1" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M16,12A2,2 0 0,1 18,10A2,2 0 0,1 20,12A2,2 0 0,1 18,14A2,2 0 0,1 16,12M10,12A2,2 0 0,1 12,10A2,2 0 0,1 14,12A2,2 0 0,1 12,14A2,2 0 0,1 10,12M4,12A2,2 0 0,1 6,10A2,2 0 0,1 8,12A2,2 0 0,1 6,14A2,2 0 0,1 4,12Z"/>
                </svg>
                <span class="text-xs">چالش‌ها</span>
            </button>
            <button class="black-card p-3 rounded-xl shadow-lg hover:shadow-xl transition duration-200 flex-1 max-w-24 border border-yellow-500 text-yellow-400">
                <svg class="w-6 h-6 mx-auto mb-1" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M13,3V9H21V3M13,21H21V11H13M3,21H11V15H3M3,13H11V3H3V13Z"/>
                </svg>
                <span class="text-xs">تاریخچه</span>
            </button>
        </div>
    </div>

    <!-- صفحه تنظیمات -->
    <div id="settingsPage" class="hidden min-h-screen p-4">
        <div class="black-card rounded-2xl shadow-2xl p-6 max-w-md mx-auto border border-yellow-500">
            <div class="flex items-center justify-between mb-6">
                <h2 class="text-2xl font-bold text-yellow-400">تنظیمات</h2>
                <button onclick="hideSettings()" class="text-gray-400 hover:text-yellow-400">✕</button>
            </div>
            
            <div class="space-y-4">
                <button onclick="showGiftCodePanel()" class="w-full text-right p-4 hover:bg-gray-700 rounded-lg transition duration-200 text-gray-300 hover:text-yellow-400">
                    <svg class="w-5 h-5 inline-block ml-2" viewBox="0 0 24 24" fill="currentColor">
                        <path d="M12,15A3,3 0 0,1 9,12A3,3 0 0,1 12,9A3,3 0 0,1 15,12A3,3 0 0,1 12,15M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2Z"/>
                    </svg>
                    کد هدیه
                </button>
                <button onclick="showDevelopers()" class="w-full text-right p-4 hover:bg-gray-700 rounded-lg transition duration-200 text-gray-300 hover:text-yellow-400">
                    <svg class="w-5 h-5 inline-block ml-2" viewBox="0 0 24 24" fill="currentColor">
                        <path d="M16,4C16.88,4 17.67,4.5 18,5.26L19,7H20A2,2 0 0,1 22,9V20A2,2 0 0,1 20,22H4A2,2 0 0,1 2,20V9C2,7.89 2.9,7 4,7H5L6,5.26C6.33,4.5 7.12,4 8,4H16M16.5,9A1.5,1.5 0 0,0 15,10.5V11.5A1.5,1.5 0 0,0 16.5,13A1.5,1.5 0 0,0 18,11.5V10.5A1.5,1.5 0 0,0 16.5,9M12,9A4,4 0 0,0 8,13A4,4 0 0,0 12,17A4,4 0 0,0 16,13A4,4 0 0,0 12,9Z"/>
                    </svg>
                    سازندگان
                </button>
                <button class="w-full text-right p-4 hover:bg-gray-700 rounded-lg transition duration-200 text-gray-300 hover:text-yellow-400">
                    <svg class="w-5 h-5 inline-block ml-2" viewBox="0 0 24 24" fill="currentColor">
                        <path d="M12,3C16.97,3 21,7.03 21,12C21,16.97 16.97,21 12,21A9,9 0 0,1 3,12A9,9 0 0,1 12,3M12,8.5A3.5,3.5 0 0,0 8.5,12A3.5,3.5 0 0,0 12,15.5A3.5,3.5 0 0,0 15.5,12A3.5,3.5 0 0,0 12,8.5M12,13.5A1.5,1.5 0 0,1 10.5,12A1.5,1.5 0 0,1 12,10.5A1.5,1.5 0 0,1 13.5,12A1.5,1.5 0 0,1 12,13.5Z"/>
                    </svg>
                    پشتیبانی
                </button>
            </div>
        </div>
    </div>

    <!-- صفحه انتخاب مرحله -->
    <div id="levelsPage" class="hidden min-h-screen p-4">
        <div class="black-card rounded-2xl shadow-2xl p-6 max-w-2xl mx-auto border border-yellow-500">
            <div class="flex items-center justify-between mb-6">
                <h2 class="text-2xl font-bold text-yellow-400">انتخاب مرحله</h2>
                <button onclick="backToMenu()" class="text-gray-400 hover:text-yellow-400">
                    <svg class="w-6 h-6" viewBox="0 0 24 24" fill="currentColor">
                        <path d="M20,11V13H8L13.5,18.5L12.08,19.92L4.16,12L12.08,4.08L13.5,5.5L8,11H20Z"/>
                    </svg>
                </button>
            </div>
            
            <div class="grid grid-cols-5 gap-3" id="levelsGrid">
                <!-- مراحل اینجا تولید می‌شوند -->
            </div>
        </div>
    </div>

    <!-- صفحه جستجوی بازیکن -->
    <div id="searchingPage" class="hidden min-h-screen p-4">
        <div class="max-w-lg mx-auto">
            <!-- هدر -->
            <div class="black-card rounded-xl p-4 mb-6 text-center border border-yellow-500">
                <h2 class="text-2xl font-bold text-yellow-400 mb-2">جستجوی حریف</h2>
                <p class="text-gray-300 text-sm">در حال یافتن بازیکن مناسب برای شما...</p>
            </div>

            <!-- انیمیشن جستجو -->
            <div class="black-card rounded-xl p-8 mb-6 text-center border border-yellow-500">
                <div class="relative mb-6">
                    <div class="w-24 h-24 mx-auto relative">
                        <!-- دایره‌های متحرک -->
                        <div class="absolute inset-0 border-4 border-yellow-400 rounded-full animate-spin border-t-transparent"></div>
                        <div class="absolute inset-2 border-4 border-yellow-600 rounded-full animate-spin border-b-transparent" style="animation-direction: reverse; animation-duration: 1.5s;"></div>
                        <div class="absolute inset-4 border-4 border-yellow-300 rounded-full animate-spin border-l-transparent" style="animation-duration: 2s;"></div>
                        
                        <!-- آیکون وسط -->
                        <div class="absolute inset-0 flex items-center justify-center">
                            <svg class="w-8 h-8 text-yellow-400" viewBox="0 0 24 24" fill="currentColor">
                                <path d="M15.5,12C18,12 20,14 20,16.5C20,17.38 19.75,18.21 19.31,18.9L22.39,22L21,23.39L17.88,20.32C17.19,20.75 16.37,21 15.5,21C13,21 11,19 11,16.5C11,14 13,12 15.5,12M15.5,14A2.5,2.5 0 0,0 13,16.5A2.5,2.5 0 0,0 15.5,19A2.5,2.5 0 0,0 18,16.5A2.5,2.5 0 0,0 15.5,14M10,4A4,4 0 0,1 14,8C14,8.91 13.69,9.75 13.18,10.43C12.32,10.75 11.55,11.26 10.91,11.9L10,12A4,4 0 0,1 6,8A4,4 0 0,1 10,4M2,20V18C2,15.88 5.31,14.14 9.5,14C9.18,14.78 9,15.62 9,16.5C9,17.79 9.38,19 10,20H2Z"/>
                            </svg>
                        </div>
                    </div>
                </div>

                <div class="space-y-3">
                    <div class="flex items-center justify-center space-x-2 space-x-reverse">
                        <div class="w-2 h-2 bg-yellow-400 rounded-full animate-bounce"></div>
                        <div class="w-2 h-2 bg-yellow-400 rounded-full animate-bounce" style="animation-delay: 0.1s"></div>
                        <div class="w-2 h-2 bg-yellow-400 rounded-full animate-bounce" style="animation-delay: 0.2s"></div>
                        <div class="w-2 h-2 bg-yellow-400 rounded-full animate-bounce" style="animation-delay: 0.3s"></div>
                        <div class="w-2 h-2 bg-yellow-400 rounded-full animate-bounce" style="animation-delay: 0.4s"></div>
                    </div>
                    <p class="text-yellow-400 font-medium" id="searchStatus">جستجوی بازیکنان آنلاین...</p>
                </div>
            </div>

            <!-- آمار جستجو -->
            <div class="black-card rounded-xl p-4 mb-6 border border-yellow-500">
                <div class="grid grid-cols-2 gap-4 text-center">
                    <div>
                        <div class="text-2xl font-bold text-green-400" id="searchTime">12</div>
                        <div class="text-xs text-gray-400">ثانیه</div>
                    </div>
                    <div>
                        <div class="text-2xl font-bold text-blue-400" id="foundCount">3</div>
                        <div class="text-xs text-gray-400">یافت شده</div>
                    </div>
                </div>
            </div>

            <!-- دکمه لغو -->
            <button onclick="backToMenu()" class="w-full black-card hover:bg-gray-700 text-yellow-400 font-medium py-3 px-4 rounded-xl transition duration-200 border border-yellow-500">
                <svg class="w-5 h-5 inline-block ml-2" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M19,6.41L17.59,5L12,10.59L6.41,5L5,6.41L10.59,12L5,17.59L6.41,19L12,13.41L17.59,19L19,17.59L13.41,12L19,6.41Z"/>
                </svg>
                لغو جستجو
            </button>
        </div>
    </div>

    <!-- صفحه نمایش حریف -->
    <div id="opponentPage" class="hidden min-h-screen flex items-center justify-center p-4">
        <div class="black-card rounded-2xl shadow-2xl p-8 text-center max-w-md w-full slide-in border border-yellow-500">
            <h2 class="text-2xl font-bold text-yellow-400 mb-6">حریف پیدا شد!</h2>
            
            <div class="bg-gray-800 rounded-xl p-6 mb-6 border border-gray-600">
                <div class="profile-circle w-16 h-16 rounded-full mx-auto mb-4"></div>
              # -
