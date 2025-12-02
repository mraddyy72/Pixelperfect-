<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Remove Background with High Quality and Quick</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap');
        
        body { font-family:
        'Inter', sans-serif; }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 10px; }
        ::-webkit-scrollbar-track { background: #f1f5f9; }
        ::-webkit-scrollbar-thumb { background: #3b82f6; border-radius: 5px; }
        ::-webkit-scrollbar-thumb:hover { background: #2563eb; }

        /* Transparency Checkerboard Pattern */
        .bg-transparency {
            background-image: 
                linear-gradient(45deg, #e5e7eb 25%, transparent 25%), 
                linear-gradient(-45deg, #e5e7eb 25%, transparent 25%), 
                linear-gradient(45deg, transparent 75%, #e5e7eb 75%), 
                linear-gradient(-45deg, transparent 75%, #e5e7eb 75%);
            background-size: 20px 20px;
            background-position: 0 0, 0 10px, 10px -10px, -10px 0px;
            background-color: white;
        }

        /* Comparison Slider Styles */
        .comparison-container {
            position: relative;
            overflow: hidden;
            border-radius: 1rem;
            cursor: col-resize;
            user-select: none;
        }
        
        /* The draggable handle line */
        .slider-line {
            position: absolute;
            top: 0;
            bottom: 0;
            left: 50%;
            width: 2px;
            background: white;
            z-index: 30;
            pointer-events: none; /* Let clicks pass through */
            box-shadow: 0 0 10px rgba(0,0,0,0.3);
        }

        /* The circular handle button */
        .slider-button {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 40px;
            height: 40px;
            background: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.2);
            z-index: 40;
            color: #2563eb;
            pointer-events: none;
        }

        /* Animations */
        .fade-in-up { animation: fadeInUp 0.8s ease-out forwards; opacity: 0; transform: translateY(20px); }
        .delay-100 { animation-delay: 0.1s; }
        .delay-200 { animation-delay: 0.2s; }
        @keyframes fadeInUp { to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 antialiased" onload="initComparisons()">

    <!-- Notification Toast -->
    <div id="toast" class="fixed top-5 right-5 z-50 transform translate-x-full transition-transform duration-300 ease-in-out bg-white border-l-4 border-blue-500 shadow-lg rounded-lg p-4 flex items-center gap-3 hidden">
        <div class="text-blue-500"><i class="fas fa-check-circle text-xl"></i></div>
        <div>
            <h4 class="font-bold text-gray-800">Order Sent!</h4>
            <p class="text-sm text-gray-600">I will contact you shortly.</p>
        </div>
    </div>

    <!-- Navigation -->
    <nav class="fixed w-full z-40 bg-white/90 backdrop-blur-md border-b border-slate-200 transition-all duration-300" id="navbar">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16 items-center">
                <div class="flex-shrink-0 flex items-center cursor-pointer" onclick="window.scrollTo(0,0)">
                    <span class="text-2xl font-bold tracking-tighter text-slate-900"><i class="fas fa-layer-group text-blue-600 mr-2"></i>Pixel<span class="text-blue-600">Perfect</span></span>
                </div>
                
                <div class="hidden md:flex space-x-8 items-center">
                    <a href="#services" class="text-sm font-medium text-slate-600 hover:text-blue-600 transition-colors">Services</a>
                    <a href="#portfolio" class="text-sm font-medium text-slate-600 hover:text-blue-600 transition-colors">Portfolio</a>
                    <a href="#pricing" class="text-sm font-medium text-slate-600 hover:text-blue-600 transition-colors">Pricing</a>
                    <a href="#contact" class="px-5 py-2.5 bg-blue-600 text-white text-sm font-medium rounded-full hover:bg-blue-700 transition-colors shadow-lg shadow-blue-500/20">
                        Order Now
                    </a>
                </div>

                <div class="md:hidden flex items-center">
                    <button onclick="toggleMobileMenu()" class="text-slate-600 hover:text-slate-900 focus:outline-none p-2">
                        <i class="fas fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </div>
        <!-- Mobile Menu -->
        <div id="mobile-menu" class="hidden md:hidden bg-white border-t border-slate-100 absolute w-full shadow-xl">
            <div class="px-4 pt-2 pb-6 space-y-1">
                <a href="#services" onclick="toggleMobileMenu()" class="block px-3 py-3 font-medium text-slate-600">Services</a>
                <a href="#portfolio" onclick="toggleMobileMenu()" class="block px-3 py-3 font-medium text-slate-600">Portfolio</a>
                <a href="#pricing" onclick="toggleMobileMenu()" class="block px-3 py-3 font-medium text-slate-600">Pricing</a>
                <a href="#contact" onclick="toggleMobileMenu()" class="block px-3 py-3 mt-4 text-center font-medium bg-blue-600 text-white rounded-md">Order Now</a>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="relative pt-32 pb-20 lg:pt-48 lg:pb-32 overflow-hidden bg-slate-50">
        <div class="absolute top-0 right-0 w-2/3 h-full bg-white skew-x-12 translate-x-20 z-0 opacity-50"></div>
        
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="grid lg:grid-cols-2 gap-12 items-center">
                <div class="text-left">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-blue-50 border border-blue-100 text-blue-700 text-xs font-semibold mb-6 fade-in-up">
                        <i class="fas fa-bolt text-yellow-500"></i> Fast Turnaround: Under 24 Hours
                    </div>
                    <!-- Updated Title Here -->
                    <h1 class="text-5xl lg:text-6xl font-bold tracking-tight text-slate-900 mb-6 fade-in-up delay-100 leading-tight">
                        Remove Background with <br>
                        <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-indigo-600">High Quality and Quick</span>
                    </h1>
                    <p class="text-lg text-slate-600 mb-8 fade-in-up delay-200 leading-relaxed max-w-lg">
                        I help e-commerce owners and photographers save time. High-quality clipping paths, masking, and retouching delivered with speed and precision.
                    </p>
                    <div class="flex flex-col sm:flex-row gap-4 fade-in-up delay-200">
                        <a href="#contact" class="px-8 py-4 bg-blue-600 text-white font-semibold rounded-xl hover:bg-blue-700 transition-all shadow-xl shadow-blue-500/20 text-center">
                            Order Now
                        </a>
                        <a href="#portfolio" class="px-8 py-4 bg-white text-slate-700 border border-slate-200 font-semibold rounded-xl hover:bg-slate-50 transition-all text-center">
                            View Samples
                        </a>
                    </div>
                </div>

                <!-- Simple Visual for Hero -->
                <div class="relative fade-in-up delay-200 hidden lg:block">
                    <div class="relative rounded-2xl shadow-2xl overflow-hidden border-4 border-white h-[400px]">
                        <!-- Using a placeholder image for hero visual -->
                        <img src="https://images.unsplash.com/photo-1542291026-7eec264c27ff?ixlib=rb-4.0.3&auto=format&fit=crop&w=1000&q=80" class="w-full h-full object-cover" alt="Product Shoe">
                        
                        <!-- Floating Badge -->
                        <div class="absolute bottom-8 left-8 bg-white/90 backdrop-blur px-4 py-2 rounded-lg shadow-lg z-20 border border-slate-100">
                            <div class="text-xs font-bold text-slate-400 uppercase tracking-wider">Status</div>
                            <div class="text-green-600 font-bold flex items-center gap-2"><div class="w-2 h-2 rounded-full bg-green-500"></div> Background Removed</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Services -->
    <section id="services" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-3xl font-bold text-slate-900 mb-4">My Services</h2>
                <p class="text-slate-600">Specialized services designed for Amazon, eBay, Shopify sellers, and photographers.</p>
            </div>
            <div class="grid md:grid-cols-3 gap-8">
                <div class="p-8 rounded-2xl bg-slate-50 border border-slate-100 hover:border-blue-200 transition-colors">
                    <div class="w-12 h-12 bg-blue-100 text-blue-600 rounded-lg flex items-center justify-center text-xl mb-6"><i class="fas fa-cut"></i></div>
                    <h3 class="text-xl font-bold text-slate-900 mb-3">Background Removal</h3>
                    <p class="text-slate-600 text-sm">Precision clipping paths for complex edges. Delivered on transparent or white backgrounds.</p>
                </div>
                <div class="p-8 rounded-2xl bg-slate-50 border border-slate-100 hover:border-blue-200 transition-colors">
                    <div class="w-12 h-12 bg-purple-100 text-purple-600 rounded-lg flex items-center justify-center text-xl mb-6"><i class="fas fa-ghost"></i></div>
                    <h3 class="text-xl font-bold text-slate-900 mb-3">Ghost Mannequin</h3>
                    <p class="text-slate-600 text-sm">Create a 3D hollow man effect for clothing to give your apparel a professional shape.</p>
                </div>
                <div class="p-8 rounded-2xl bg-slate-50 border border-slate-100 hover:border-blue-200 transition-colors">
                    <div class="w-12 h-12 bg-emerald-100 text-emerald-600 rounded-lg flex items-center justify-center text-xl mb-6"><i class="fas fa-sun"></i></div>
                    <h3 class="text-xl font-bold text-slate-900 mb-3">Shadow & Reflection</h3>
                    <p class="text-slate-600 text-sm">Adding natural drop shadows or mirror reflections to ground your products.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Portfolio Comparison Section -->
    <section id="portfolio" class="py-20 bg-slate-900 text-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <span class="text-blue-400 font-semibold tracking-wider text-sm uppercase">See The Quality</span>
                <h2 class="text-3xl md:text-4xl font-bold mt-2">Interactive Demo</h2>
                <p class="text-slate-400 mt-4">Drag the slider to see the precision.</p>
            </div>

            <div class="grid md:grid-cols-2 gap-12">
                
                <!-- Demo 1 -->
                <div>
                    <div class="comparison-container h-[400px] w-full bg-transparency relative group rounded-2xl shadow-2xl">
                        <!-- AFTER Image -->
                        <div class="absolute inset-0 w-full h-full">
                            <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" class="w-full h-full object-cover grayscale opacity-50 after-img" alt="After">
                            <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
                                <span class="bg-black/50 px-3 py-1 rounded text-sm font-bold">TRANSPARENT</span>
                            </div>
                        </div>
                        <!-- BEFORE Image -->
                        <div class="img-overlay absolute inset-0 w-[50%] h-full overflow-hidden border-r-2 border-white z-20">
                            <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" class="absolute top-0 left-0 h-full max-w-none w-auto before-img-responsive" alt="Before">
                        </div>
                        <!-- Slider Handle -->
                        <div class="slider-handle slider-line"></div>
                        <div class="slider-handle slider-button"><i class="fas fa-arrows-alt-h"></i></div>
                    </div>
                    <div class="mt-4 flex justify-between text-sm text-slate-400">
                        <span>Original Photo</span>
                        <span>Background Removed</span>
                    </div>
                </div>

                <!-- Demo 2 -->
                <div>
                    <div class="comparison-container h-[400px] w-full bg-transparency relative group rounded-2xl shadow-2xl">
                        <!-- AFTER Image -->
                        <div class="absolute inset-0 w-full h-full">
                             <img src="https://images.unsplash.com/photo-1505740420928-5e560c06d30e?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" class="w-full h-full object-cover grayscale opacity-50 after-img" alt="After">
                             <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
                                <span class="bg-black/50 px-3 py-1 rounded text-sm font-bold">TRANSPARENT</span>
                            </div>
                        </div>
                        <!-- BEFORE Image -->
                        <div class="img-overlay absolute inset-0 w-[50%] h-full overflow-hidden border-r-2 border-white z-20">
                             <img src="https://images.unsplash.com/photo-1505740420928-5e560c06d30e?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" class="absolute top-0 left-0 h-full max-w-none w-auto before-img-responsive" alt="Before">
                        </div>
                        <!-- Handle -->
                        <div class="slider-handle slider-line"></div>
                        <div class="slider-handle slider-button"><i class="fas fa-arrows-alt-h"></i></div>
                    </div>
                    <div class="mt-4 flex justify-between text-sm text-slate-400">
                        <span>Original Photo</span>
                        <span>Clean Cut</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Pricing Section -->
    <section id="pricing" class="py-20 bg-slate-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-3xl font-bold text-slate-900">Affordable Packages</h2>
                <p class="text-slate-600 mt-4">Simple pricing per batch. Choose the package that suits your needs.</p>
            </div>

            <div class="grid md:grid-cols-3 gap-8 max-w-5xl mx-auto items-center">
                <!-- BASIC -->
                <div class="bg-white p-8 rounded-2xl shadow-sm border border-slate-100 hover:shadow-md transition-shadow">
                    <h3 class="font-bold text-slate-900 text-xl tracking-wide uppercase text-center mb-4">Basic</h3>
                    <div class="text-center mb-6 py-6 bg-slate-50 rounded-xl border border-slate-100">
                        <span class="block text-sm text-slate-500 font-semibold uppercase mb-1">Total Cost</span>
                        <span class="text-5xl font-bold text-slate-900">$5</span>
                    </div>
                    <div class="text-center mb-8">
                        <p class="text-lg font-bold text-slate-800 mb-1">5 Images Included</p>
                        <p class="text-sm text-slate-500">($1.00 per image)</p>
                    </div>
                    <a href="#contact" class="block w-full py-3 text-center border-2 border-slate-200 text-slate-700 rounded-xl font-bold hover:border-blue-600 hover:text-blue-600 transition-colors">Select Basic</a>
                </div>

                <!-- STANDARD -->
                <div class="bg-white p-8 rounded-2xl shadow-xl border-2 border-blue-600 relative transform md:-translate-y-4">
                    <div class="absolute top-0 right-0 bg-blue-600 text-white text-xs font-bold px-3 py-1 rounded-bl-lg rounded-tr-lg">MOST POPULAR</div>
                    <h3 class="font-bold text-blue-600 text-xl tracking-wide uppercase text-center mb-4">Standard</h3>
                    <div class="text-center mb-6 py-6 bg-blue-50 rounded-xl border border-blue-100">
                        <span class="block text-sm text-blue-600 font-semibold uppercase mb-1">Total Cost</span>
                        <span class="text-6xl font-bold text-slate-900">$10</span>
                    </div>
                    <div class="text-center mb-8">
                        <p class="text-xl font-bold text-slate-800 mb-1">15 Images Included</p>
                        <p class="text-sm text-slate-500">($0.66 per image)</p>
                    </div>
                    <a href="#contact" class="block w-full py-4 text-center bg-blue-600 text-white rounded-xl font-bold hover:bg-blue-700 transition-colors shadow-lg shadow-blue-500/30">Select Standard</a>
                </div>

                <!-- PREMIUM -->
                <div class="bg-white p-8 rounded-2xl shadow-sm border border-slate-100 hover:shadow-md transition-shadow">
                    <h3 class="font-bold text-slate-900 text-xl tracking-wide uppercase text-center mb-4">Premium</h3>
                    <div class="text-center mb-6 py-6 bg-slate-50 rounded-xl border border-slate-100">
                        <span class="block text-sm text-slate-500 font-semibold uppercase mb-1">Total Cost</span>
                        <span class="text-5xl font-bold text-slate-900">$15</span>
                    </div>
                    <div class="text-center mb-8">
                        <p class="text-lg font-bold text-slate-800 mb-1">30 Images Included</p>
                        <p class="text-sm text-slate-500">($0.50 per image)</p>
                    </div>
                    <a href="#contact" class="block w-full py-3 text-center border-2 border-slate-200 text-slate-700 rounded-xl font-bold hover:border-blue-600 hover:text-blue-600 transition-colors">Select Premium</a>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-24 bg-white">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="bg-blue-600 rounded-3xl overflow-hidden shadow-2xl flex flex-col md:flex-row">
                <div class="p-10 text-white md:w-2/5 flex flex-col justify-between">
                    <div>
                        <h2 class="text-3xl font-bold mb-4">Place Your Order</h2>
                        <p class="text-blue-100 mb-8">Fill out the form and I'll get back to you with a confirmation.</p>
                        <div c# Pixelperfect-
