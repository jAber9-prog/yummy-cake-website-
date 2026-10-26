# yummy-cake-website-
import React, { useState } from 'react';
import { 
  ShoppingBag, 
  MessageCircle, 
  Send, 
  Menu as MenuIcon, 
  X, 
  Heart, 
  CheckCircle2, 
  Clock, 
  Truck, 
  Sparkles, 
  ChefHat, 
  Phone, 
  Filter,
  ArrowRight
} from 'lucide-react';

// Main Application Component
export default function App() {
  const [activeTab, setActiveTab] = useState('home');
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [selectedShape, setSelectedShape] = useState('all');
  const [selectedFlavor, setSelectedFlavor] = useState('all');
  const [orderModalCake, setOrderModalCake] = useState(null);
  const [customNotes, setCustomNotes] = useState('');

  // Contact details
  const whatsappNumber = "8801700000000"; // Replace with real WhatsApp number
  const messengerUrl = "https://m.me/yummycakekhulna"; // Replace with real Facebook Messenger link

  // Cake Catalog Data
  const cakes = [
    {
      id: 1,
      name: "2 Pounds Chocolate Signature Cake",
      flavor: "Chocolate",
      shape: "Round",
      price: 1490,
      badge: "Best Seller",
      image: "https://images.unsplash.com/photo-1578985545062-69928b1d9587?auto=format&fit=crop&q=80&w=800",
      description: "Rich, moist homemade chocolate layers coated with decadent cocoa frosting. Made fresh only upon receiving your order."
    },
    {
      id: 2,
      name: "2 Pounds Chocolate Love Shape Cake",
      flavor: "Chocolate",
      shape: "Love",
      price: 1490,
      badge: "Popular",
      image: "https://images.unsplash.com/photo-1606890737304-57a1ca8a5b62?auto=format&fit=crop&q=80&w=800",
      description: "Heart-shaped rich chocolate cake created with love. Perfect for anniversaries, birthdays, and special surprises."
    },
    {
      id: 3,
      name: "2 Pounds Chocolate Square Shape Cake",
      flavor: "Chocolate",
      shape: "Square",
      price: 1490,
      badge: "Classic",
      image: "https://images.unsplash.com/photo-1558301211-0d8c8ddee6ec?auto=format&fit=crop&q=80&w=800",
      description: "Clean square cut 2-pound chocolate delight with smooth chocolate ganache frosting."
    },
    {
      id: 4,
      name: "2 Pounds Classic Vanilla Cake",
      flavor: "Vanilla",
      shape: "Round",
      price: 1290,
      badge: "Classic",
      image: "https://images.unsplash.com/photo-1535141192574-5d4897c13136?auto=format&fit=crop&q=80&w=800",
      description: "Light, fluffy vanilla sponge crafted with premium vanilla bean essence and fresh whipped cream."
    },
    {
      id: 5,
      name: "2 Pounds Vanilla Love Shape Cake",
      flavor: "Vanilla",
      shape: "Love",
      price: 1290,
      badge: "Special",
      image: "https://images.unsplash.com/photo-1565958011703-44f9829ba187?auto=format&fit=crop&q=80&w=800",
      description: "Elegant heart-shaped vanilla cake decorated with soft vanilla cream swirls and delicate touches."
    },
    {
      id: 6,
      name: "2 Pounds Vanilla Square Shape Cake",
      flavor: "Vanilla",
      shape: "Square",
      price: 1290,
      badge: "Modern",
      image: "https://images.unsplash.com/photo-1588195538326-c5b1e9f80a1b?auto=format&fit=crop&q=80&w=800",
      description: "Minimalist square vanilla sponge cake freshly prepared with pure butter and real vanilla extracts."
    },
    {
      id: 7,
      name: "2 Pounds Premium Berry / Strawberry Cream Cake",
      flavor: "Berry",
      shape: "Round",
      price: 1490,
      badge: "Chef Special",
      image: "https://images.unsplash.com/photo-1563729784474-d77dbb933a9e?auto=format&fit=crop&q=80&w=800",
      description: "Fresh vanilla layers topped with strawberries & fresh berries. Pure ingredients, real taste!"
    }
  ];

  // Helper to construct pre-filled WhatsApp link
  const getWhatsAppLink = (cake, shape = cake?.shape, notes = '') => {
    const text = encodeURIComponent(
      `Hello Yummy Cake ðŸ‘‹\nI would like to order a cake:\n\nðŸŽ‚ Item: ${cake.name}\nâš–ï¸ Weight: 2 Pounds\nðŸ“ Shape: ${shape} Shape\nðŸ’µ Price: à§³${cake.price}\nðŸ“ Location: Khulna City\n${notes ? `ðŸ“ Note: ${notes}\n` : ''}\nPlease confirm my order status!`
    );
    return `https://wa.me/${whatsappNumber}?text=${text}`;
  };

  // Filter logic
  const filteredCakes = cakes.filter(cake => {
    const matchShape = selectedShape === 'all' || cake.shape.toLowerCase() === selectedShape.toLowerCase();
    const matchFlavor = selectedFlavor === 'all' || cake.flavor.toLowerCase() === selectedFlavor.toLowerCase();
    return matchShape && matchFlavor;
  });

  return (
    <div className="min-h-screen bg-[#FAF7F2] text-[#3D2C24] font-sans antialiased flex flex-col selection:bg-[#E2C7B8] selection:text-[#3D2C24]">
      
      {/* 1. TOP ANNOUNCEMENT BAR */}
      <div className="bg-[#4A2E20] text-[#F3EAD8] text-xs md:text-sm py-2 px-4 text-center font-medium tracking-wide flex items-center justify-center gap-2 shadow-inner">
        <Truck className="w-4 h-4 text-[#D97757] animate-bounce" />
        <span>Khulna City te Jekono Jaigai <strong>Delivery Charge Free!</strong> | Minimum Order: <strong>2 Pounds</strong></span>
      </div>

      {/* 2. HEADER / NAVIGATION */}
      <header className="sticky top-0 z-40 bg-[#FAF7F2]/90 backdrop-blur-md border-b border-[#E8DFC8]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
          
          {/* Brand Logo & Name */}
          <div 
            onClick={() => setActiveTab('home')}
            className="flex items-center gap-3 cursor-pointer group"
          >
            <div className="w-12 h-12 rounded-full bg-[#FAF3E0] border-2 border-[#8C533E] flex items-center justify-center shadow-md group-hover:scale-105 transition-transform">
              <ChefHat className="w-7 h-7 text-[#8C533E]" />
            </div>
            <div>
              <h1 className="text-xl md:text-2xl font-serif font-bold text-[#4A2E20] leading-none tracking-tight">
                Yummy Cake
              </h1>
              <p className="text-xs text-[#8C6F61] font-medium tracking-wide mt-0.5">
                We Care About Every Bite â€¢ Homemade with Love
              </p>
            </div>
          </div>

          {/* Desktop Navigation Links */}
          <nav className="hidden md:flex items-center gap-8 text-sm font-semibold text-[#5C4336]">
            <button 
              onClick={() => setActiveTab('home')}
              className={`hover:text-[#8C533E] transition-colors py-1 relative ${activeTab === 'home' ? 'text-[#8C533E] font-bold border-b-2 border-[#8C533E]' : ''}`}
            >
              Home
            </button>
            <button 
              onClick={() => setActiveTab('menu')}
              className={`hover:text-[#8C533E] transition-colors py-1 relative ${activeTab === 'menu' ? 'text-[#8C533E] font-bold border-b-2 border-[#8C533E]' : ''}`}
            >
              Menu & Catalog
            </button>
            <button 
              onClick={() => setActiveTab('policy')}
              className={`hover:text-[#8C533E] transition-colors py-1 relative ${activeTab === 'policy' ? 'text-[#8C533E] font-bold border-b-2 border-[#8C533E]' : ''}`}
            >
              Order Policy
            </button>
            <button 
              onClick={() => setActiveTab('contact')}
              className={`hover:text-[#8C533E] transition-colors py-1 relative ${activeTab === 'contact' ? 'text-[#8C533E] font-bold border-b-2 border-[#8C533E]' : ''}`}
            >
              Contact
            </button>
          </nav>

          {/* Direct Social & Quick Action Buttons */}
          <div className="hidden lg:flex items-center gap-3">
            <a 
              href={`https://wa.me/${whatsappNumber}`} 
              target="_blank" 
              rel="noreferrer"
              className="bg-[#25D366] hover:bg-[#20bd5a] text-white px-4 py-2 rounded-full text-xs font-bold flex items-center gap-2 shadow-sm hover:shadow transition-all"
            >
              <MessageCircle className="w-4 h-4" />
              WhatsApp Us
            </a>
            <a 
              href={messengerUrl} 
              target="_blank" 
              rel="noreferrer"
              className="bg-[#0084FF] hover:bg-[#0074e0] text-white px-4 py-2 rounded-full text-xs font-bold flex items-center gap-2 shadow-sm hover:shadow transition-all"
            >
              <Send className="w-4 h-4" />
              Messenger
            </a>
          </div>

          {/* Mobile Menu Button */}
          <button 
            onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
            className="md:hidden p-2 rounded-lg text-[#4A2E20] hover:bg-[#EFE8D8] transition-colors"
          >
            {mobileMenuOpen ? <X className="w-6 h-6" /> : <MenuIcon className="w-6 h-6" />}
          </button>
        </div>

        {/* Mobile Navigation Drawer */}
        {mobileMenuOpen && (
          <div className="md:hidden bg-[#FAF7F2] border-b border-[#E8DFC8] px-4 pt-2 pb-6 space-y-3 animate-fadeIn">
            <button 
              onClick={() => { setActiveTab('home'); setMobileMenuOpen(false); }}
              className={`block w-full text-left py-2 px-3 rounded-md font-medium ${activeTab === 'home' ? 'bg-[#EFE8D8] text-[#8C533E]' : 'text-[#4A2E20]'}`}
            >
              Home
            </button>
            <button 
              onClick={() => { setActiveTab('menu'); setMobileMenuOpen(false); }}
              className={`block w-full text-left py-2 px-3 rounded-md font-medium ${activeTab === 'menu' ? 'bg-[#EFE8D8] text-[#8C533E]' : 'text-[#4A2E20]'}`}
            >
              Menu & Catalog
            </button>
            <button 
              onClick={() => { setActiveTab('policy'); setMobileMenuOpen(false); }}
              className={`block w-full text-left py-2 px-3 rounded-md font-medium ${activeTab === 'policy' ? 'bg-[#EFE8D8] text-[#8C533E]' : 'text-[#4A2E20]'}`}
            >
              Order Policy
            </button>
            <button 
              onClick={() => { setActiveTab('contact'); setMobileMenuOpen(false); }}
              className={`block w-full text-left py-2 px-3 rounded-md font-medium ${activeTab === 'contact' ? 'bg-[#EFE8D8] text-[#8C533E]' : 'text-[#4A2E20]'}`}
            >
              Contact Us
            </button>
            
            <div className="pt-2 flex flex-col gap-2">
              <a 
                href={`https://wa.me/${whatsappNumber}`} 
                target="_blank" 
                rel="noreferrer"
                className="w-full bg-[#25D366] text-white py-2.5 rounded-lg text-sm font-bold flex items-center justify-center gap-2 shadow-sm"
              >
                <MessageCircle className="w-4 h-4" />
                Order via WhatsApp
              </a>
              <a 
                href={messengerUrl} 
                target="_blank" 
                rel="noreferrer"
                className="w-full bg-[#0084FF] text-white py-2.5 rounded-lg text-sm font-bold flex items-center justify-center gap-2 shadow-sm"
              >
                <Send className="w-4 h-4" />
                Message on Facebook
              </a>
            </div>
          </div>
        )}
      </header>

      {/* MAIN CONTENT CONTAINER */}
      <main className="flex-1">

        {/* ========================================================= */}
        {/* PAGE 1: HOME PAGE */}
        {/* ========================================================= */}
        {activeTab === 'home' && (
          <div>
            {/* HERO BANNER SECTION */}
            <section className="relative overflow-hidden py-16 lg:py-24 bg-[#F4EDE2] border-b border-[#E5DAC6]">
              <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div className="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                  
                  {/* Left Column Text */}
                  <div className="space-y-6 text-center lg:text-left">
                    <div className="inline-flex items-center gap-2 bg-[#EADCC9] text-[#6E4230] px-4 py-1.5 rounded-full text-xs font-semibold uppercase tracking-wider">
                      <Sparkles className="w-3.5 h-3.5 text-[#8C533E]" />
                      Authentic Homemade Baking
                    </div>
                    <h1 className="text-4xl sm:text-5xl lg:text-6xl font-serif font-bold text-[#3D2C24] leading-tight">
                      Pure Ingredients.<br />
                      Real Taste.<br />
                      <span className="text-[#8C533E] underline decoration-[#D97757]/30 decoration-wavy">Homemade Always.</span>
                    </h1>
                    <p className="text-base sm:text-lg text-[#6E5A4F] max-w-xl mx-auto lg:mx-0 leading-relaxed">
                      Amra shudhu matro order pelei fresh cake bake kori. High quality fresh ingredients abong hygiene maintain kore toiri hoy amader protiti cake.
                    </p>

                    {/* Policy Highlights Pill */}
                    <div className="pt-2 flex flex-wrap justify-center lg:justify-start gap-4 text-xs font-semibold text-[#5C4336]">
                      <span className="bg-[#FAF7F2] border border-[#DCD1BA] px-3.5 py-2 rounded-lg flex items-center gap-2 shadow-sm">
                        <CheckCircle2 className="w-4 h-4 text-[#8C533E]" /> 2 Pounds Minimum Order
                      </span>
                      <span className="bg-[#FAF7F2] border border-[#DCD1BA] px-3.5 py-2 rounded-lg flex items-center gap-2 shadow-sm">
                        <Clock className="w-4 h-4 text-[#8C533E]" /> Baked Fresh On Order
                      </span>
                      <span className="bg-[#FAF7F2] border border-[#DCD1BA] px-3.5 py-2 rounded-lg flex items-center gap-2 shadow-sm">
                        <Truck className="w-4 h-4 text-[#8C533E]" /> Free Delivery in Khulna
                      </span>
                    </div>

                    {/* CTA Buttons */}
                    <div className="pt-4 flex flex-col sm:flex-row items-center justify-center lg:justify-start gap-4">
                      <button 
                        onClick={() => setActiveTab('menu')}
                        className="w-full sm:w-auto bg-[#8C533E] hover:bg-[#734230] text-white px-8 py-3.5 rounded-full font-medium text-sm transition-all shadow-md hover:shadow-lg flex items-center justify-center gap-2"
                      >
                        Explore Menu & Catalog
                        <ArrowRight className="w-4 h-4" />
                      </button>
                      <a 
                        href={`https://wa.me/${whatsappNumber}`}
                        target="_blank"
                        rel="noreferrer"
                        className="w-full sm:w-auto border-2 border-[#8C533E] text-[#8C533E] hover:bg-[#8C533E] hover:text-white px-8 py-3.5 rounded-full font-medium text-sm transition-all flex items-center justify-center gap-2"
                      >
                        <MessageCircle className="w-4 h-4" />
                        Order via WhatsApp
                      </a>
                    </div>
                  </div>

                  {/* Right Column Image Banner */}
                  <div className="relative flex justify-center">
                    <div className="relative w-full max-w-md lg:max-w-none">
                      <div className="absolute -inset-4 rounded-3xl bg-gradient-to-r from-[#E8C5B0] to-[#E5DAC6] opacity-60 blur-xl"></div>
                      <div className="relative rounded-2xl overflow-hidden shadow-2xl border-4 border-[#FAF7F2]">
                        <img 
                          src="https://images.unsplash.com/photo-1578985545062-69928b1d9587?auto=format&fit=crop&q=80&w=1000" 
                          alt="Yummy Cake Chocolate Special" 
                          className="w-full h-[380px] sm:h-[450px] object-cover hover:scale-105 transition-transform duration-700"
                        />
                        <div className="absolute bottom-4 left-4 right-4 bg-[#3D2C24]/85 backdrop-blur-sm text-white p-4 rounded-xl flex items-center justify-between border border-white/10">
                          <div>
                            <p className="text-xs text-[#E2C7B8] uppercase tracking-wider font-semibold">Special Featured</p>
                            <p className="text-lg font-serif font-bold">2 Pounds Chocolate Cake</p>
                          </div>
                          <span className="text-xl font-bold text-[#E2C7B8]">à§³1,490</span>
                        </div>
                      </div>
                    </div>
                  </div>

                </div>
              </div>
            </section>

            {/* FEATURED SPOTLIGHT SECTION */}
            <section className="py-16 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
              <div className="text-center max-w-2xl mx-auto mb-12">
                <h2 className="text-3xl font-serif font-bold text-[#4A2E20]">Featured 2 Pounds Chocolate Cake</h2>
                <div className="w-16 h-1 bg-[#8C533E] mx-auto my-3 rounded-full"></div>
                <p className="text-sm text-[#6E5A4F]">
                  Amader sobcheye popular premium chocolate cake. Chocolate lover-der jonno ekdom perfect taste & quality.
                </p>
              </div>

              {/* Spotlight Card */}
              <div className="bg-white rounded-2xl shadow-xl overflow-hidden border border-[#E8DFC8] grid grid-cols-1 md:grid-cols-2">
                <div className="relative h-72 md:h-auto overflow-hidden">
                  <img 
                    src={cakes[0].image} 
                    alt={cakes[0].name}
                    className="w-full h-full object-cover"
                  />
                  <div className="absolute top-4 left-4 bg-[#8C533E] text-white text-xs font-bold px-3 py-1 rounded-full uppercase tracking-wider">
                    Most Popular
                  </div>
                </div>

                <div className="p-8 sm:p-10 flex flex-col justify-between bg-gradient-to-br from-white to-[#FAF6EE]">
                  <div className="space-y-4">
                    <div className="flex justify-between items-start">
                      <div>
                        <span className="text-xs font-bold text-[#8C533E] uppercase tracking-wider">Homemade Special</span>
                        <h3 className="text-2xl font-serif font-bold text-[#3D2C24]">{cakes[0].name}</h3>
                      </div>
                      <span className="text-2xl font-bold text-[#4A2E20] bg-[#FAF3E0] px-4 py-1.5 rounded-lg border border-[#E8DFC8]">
                        à§³{cakes[0].price}
                      </span>
                    </div>

                    <p className="text-sm text-[#6E5A4F] leading-relaxed">
                      {cakes[0].description} Rich cocoa sponge layered with velvety homemade chocolate cream. Made only on order to guarantee maximum freshness.
                    </p>

                    <div className="space-y-2 pt-2 text-xs font-medium text-[#5C4336]">
                      <div className="flex items-center gap-2">
                        <CheckCircle2 className="w-4 h-4 text-[#8C533E]" />
                        <span><strong>Weight:</strong> 2 Pounds (Minimum order size)</span>
                      </div>
                      <div className="flex items-center gap-2">
                        <CheckCircle2 className="w-4 h-4 text-[#8C533E]" />
                        <span><strong>Delivery:</strong> Right Now Delivery Free All of Khulna</span>
                      </div>
                      <div className="flex items-center gap-2">
                        <CheckCircle2 className="w-4 h-4 text-[#8C533E]" />
                        <span><strong>Custom Shape:</strong> Round, Love Shape or Square available</span>
                      </div>
                    </div>
                  </div>

                  <div className="pt-8 flex flex-col sm:flex-row gap-3">
                    <button 
                      onClick={() => setOrderModalCake(cakes[0])}
                      className="flex-1 bg-[#25D366] hover:bg-[#20bd5a] text-white py-3 rounded-xl font-bold text-sm flex items-center justify-center gap-2 shadow-sm transition-all"
                    >
                      <MessageCircle className="w-4 h-4" />
                      Order via WhatsApp
                    </button>
                    <a 
                      href={messengerUrl}
                      target="_blank"
                      rel="noreferrer"
                      className="flex-1 bg-[#0084FF] hover:bg-[#0074e0] text-white py-3 rounded-xl font-bold text-sm flex items-center justify-center gap-2 shadow-sm transition-all text-center"
                    >
                      <Send className="w-4 h-4" />
                      Order via Messenger
                    </a>
                  </div>
                </div>
              </div>
            </section>

            {/* WHY CHOOSE US / BRAND VALUES */}
            <section className="py-16 bg-[#F4EDE2] border-t border-[#E5DAC6]">
              <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div className="grid grid-cols-1 md:grid-cols-3 gap-8 text-center">
                  
                  <div className="p-6 bg-[#FAF7F2] rounded-xl border border-[#E5DAC6] shadow-sm">
                    <div className="w-12 h-12 bg-[#EADCC9] rounded-full flex items-center justify-center mx-auto mb-4">
                      <ChefHat className="w-6 h-6 text-[#8C533E]" />
                    </div>
                    <h4 className="font-serif font-bold text-lg text-[#3D2C24] mb-2">Baked Fresh On Order</h4>
                    <p className="text-xs text-[#6E5A4F] leading-relaxed">
                      Amra ager theke cake banaye rakhi na. Aapnar order confirm haowar por-i freshly bake kora hoy.
                    </p>
                  </div>

                  <div className="p-6 bg-[#FAF7F2] rounded-xl border border-[#E5DAC6] shadow-sm">
                    <div className="w-12 h-12 bg-[#EADCC9] rounded-full flex items-center justify-center mx-auto mb-4">
                      <Heart className="w-6 h-6 text-[#8C533E]" />
                    </div>
                    <h4 className="font-serif font-bold text-lg text-[#3D2C24] mb-2">Pure & Premium Ingredients</h4>
                    <p className="text-xs text-[#6E5A4F] leading-relaxed">
                      Konorokom artificial flavor ba preservative chara pure butter, milk, cocoa ebong fresh cream bebohar kora hoy.
                    </p>
                  </div>

                  <div className="p-6 bg-[#FAF7F2] rounded-xl border border-[#E5DAC6] shadow-sm">
                    <div className="w-12 h-12 bg-[#EADCC9] rounded-full flex items-center justify-center mx-auto mb-4">
                      <Truck className="w-6 h-6 text-[#8C533E]" />
                    </div>
                    <h4 className="font-serif font-bold text-lg text-[#3D2C24] mb-2">Free Delivery in Khulna</h4>
                    <p className="text-xs text-[#6E5A4F] leading-relaxed">
                      Khulna city-r jekono jaigay aapnar cake shothik shomoy ebong jotno shohokare pouchay dewa hoy delivery charge chara.
                    </p>
                  </div>

                </div>
              </div>
            </section>
          </div>
        )}

        {/* ========================================================= */}
        {/* PAGE 2: MENU & CATALOG PAGE */}
        {/* ========================================================= */}
        {activeTab === 'menu' && (
          <div className="py-12 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            
            {/* Catalog Header */}
            <div className="text-center max-w-2xl mx-auto mb-10">
              <h2 className="text-3xl font-serif font-bold text-[#4A2E20]">Our 2 Pounds Cake Collection</h2>
              <div className="w-16 h-1 bg-[#8C533E] mx-auto my-3 rounded-full"></div>
              <p className="text-sm text-[#6E5A4F]">
                Amra 2 pounds-er niche kono order nei na. Neche aapnar pochondomoto Flavor ebong Shape select kore direct order korun.
              </p>
            </div>

            {/* FILTER CONTROLS */}
            <div className="bg-white p-6 rounded-2xl shadow-sm border border-[#E8DFC8] mb-10 space-y-4">
              <div className="flex items-center gap-2 text-xs font-bold uppercase tracking-wider text-[#8C533E] border-b border-[#E8DFC8] pb-3">
                <Filter className="w-4 h-4" /> Filter By Options
              </div>

              <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                
                {/* Shape Filter */}
                <div>
                  <label className="block text-xs font-semibold text-[#5C4336] mb-2">Select Shape / Customization:</label>
                  <div className="flex flex-wrap gap-2">
                    {['all', 'Round', 'Love', 'Square'].map(shape => (
                      <button
                        key={shape}
                        onClick={() => setSelectedShape(shape)}
                        className={`px-4 py-2 rounded-lg text-xs font-semibold transition-all ${
                          selectedShape === shape 
                            ? 'bg-[#8C533E] text-white shadow-sm' 
                            : 'bg-[#FAF7F2] text-[#5C4336] border border-[#E5DAC6] hover:bg-[#EFE8D8]'
                        }`}
                      >
                        {shape === 'all' ? 'All Shapes' : shape === 'Love' ? 'Love Shape (Heart)' : `${shape} Shape`}
                      </button>
                    ))}
                  </div>
                </div>

                {/* Flavor Filter */}
                <div>
                  <label className="block text-xs font-semibold text-[#5C4336] mb-2">Select Flavor:</label>
                  <div className="flex flex-wrap gap-2">
                    {['all', 'Chocolate', 'Vanilla', 'Berry'].map(flavor => (
                      <button
                        key={flavor}
                        onClick={() => setSelectedFlavor(flavor)}
                        className={`px-4 py-2 rounded-lg text-xs font-semibold transition-all ${
                          selectedFlavor === flavor 
                            ? 'bg-[#8C533E] text-white shadow-sm' 
                            : 'bg-[#FAF7F2] text-[#5C4336] border border-[#E5DAC6] hover:bg-[#EFE8D8]'
                        }`}
                      >
                        {flavor === 'all' ? 'All Flavors' : `${flavor} Flavor`}
                      </button>
                    ))}
                  </div>
                </div>

              </div>
            </div>

            {/* CAKE CATALOG GRID */}
            <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
              {filteredCakes.map(cake => (
                <div 
                  key={cake.id} 
                  className="bg-white rounded-2xl overflow-hidden border border-[#E8DFC8] shadow-sm hover:shadow-md transition-all flex flex-col justify-between group"
                >
                  <div>
                    {/* Cake Image */}
                    <div className="relative h-56 overflow-hidden">
                      <img 
                        src={cake.image} 
                        alt={cake.name} 
                        className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500"
                      />
                      <span className="absolute top-3 left-3 bg-[#4A2E20] text-[#F3EAD8] text-[10px] font-bold px-2.5 py-1 rounded-full uppercase tracking-wider">
                        {cake.badge}
                      </span>
                      <span className="absolute bottom-3 right-3 bg-white/95 backdrop-blur-sm text-[#3D2C24] font-bold text-sm px-3 py-1 rounded-lg border border-[#E8DFC8]">
                        à§³{cake.price}
                      </span>
                    </div>

                    {/* Cake Info */}
                    <div className="p-5 space-y-3">
                      <div className="flex items-center gap-2 text-xs font-semibold text-[#8C533E]">
                        <span>{cake.flavor}</span>
                        <span>â€¢</span>
                        <span>{cake.shape} Shape</span>
                      </div>
                      <h3 className="font-serif font-bold text-lg text-[#3D2C24] leading-snug">
                        {cake.name}
                      </h3>
                      <p className="text-xs text-[#6E5A4F] leading-relaxed line-clamp-2">
                        {cake.description}
                      </p>

                      <div className="pt-2 border-t border-[#F0E8DA] flex items-center justify-between text-[11px] text-[#5C4336] font-medium">
                        <span>Weight: <strong>2 Pounds</strong></span>
                        <span className="text-[#8C533E]">Free Delivery Khulna</span>
                      </div>
                    </div>
                  </div>

                  {/* Order Button */}
                  <div className="p-5 pt-0">
                    <button 
                      onClick={() => setOrderModalCake(cake)}
                      className="w-full bg-[#8C533E] hover:bg-[#734230] text-white py-2.5 rounded-xl font-bold text-xs flex items-center justify-center gap-2 shadow-sm transition-all"
                    >
                      <ShoppingBag className="w-4 h-4" />
                      Order This Cake
                    </button>
                  </div>
                </div>
              ))}
            </div>

            {filteredCakes.length === 0 && (
              <div className="text-center py-16 bg-white rounded-2xl border border-[#E8DFC8]">
                <p className="text-gray-500">No cakes found matching your selected filters.</p>
                <button 
                  onClick={() => { setSelectedShape('all'); setSelectedFlavor('all'); }}
                  className="mt-4 text-xs text-[#8C533E] font-bold underline"
                >
                  Reset Filters
                </button>
              </div>
            )}
          </div>
        )}

        {/* ========================================================= */}
        {/* PAGE 3: ORDER POLICY */}
        {/* ========================================================= */}
        {activeTab === 'policy' && (
          <div className="py-12 max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <div className="text-center mb-10">
              <h2 className="text-3xl font-serif font-bold text-[#4A2E20]">Amader Order Policy</h2>
              <div className="w-16 h-1 bg-[#8C533E] mx-auto my-3 rounded-full"></div>
              <p className="text-sm text-[#6E5A4F]">
                Amra amader bakery-r quality ebong freshness bojay rakhTE deterministic kete kete niyam maniye chali.
              </p>
            </div>

            <div className="bg-white rounded-2xl p-8 border border-[#E8DFC8] shadow-sm space-y-6 text-sm text-[#5C4336] leading-relaxed">
              
              <div className="flex gap-4 items-start">
                <div className="w-10 h-10 rounded-full bg-[#FAF3E0] flex items-center justify-center shrink-0 border border-[#E8DFC8]">
                  <CheckCircle2 className="w-5 h-5 text-[#8C533E]" />
                </div>
                <div>
                  <h3 className="font-serif font-bold text-base text-[#3D2C24]">1. Minimum 2 Pounds Order Policy</h3>
                  <p className="mt-1 text-xs sm:text-sm text-[#6E5A4F]">
                    Amra 2 pounds-er niche kono cake order nei na. Minimum order quantity hocche 2 Pounds. Standard flavor ebong custom design shob-i 2 pound theke shuru.
                  </p>
                </div>
              </div>

              <div className="border-t border-[#F0E8DA] pt-6 flex gap-4 items-start">
                <div className="w-10 h-10 rounded-full bg-[#FAF3E0] flex items-center justify-center shrink-0 border border-[#E8DFC8]">
                  <Clock className="w-5 h-5 text-[#8C533E]" />
                </div>
                <div>
                  <h3 className="font-serif font-bold text-base text-[#3D2C24]">2. Freshly Baked On Order</h3>
                  <p className="mt-1 text-xs sm:text-sm text-[#6E5A4F]">
                    Amra kono pre-baked ba purano cake sell kori na. Aapni order confirm korle, delivery time-er shath-e match kore ekdom fresh bake kora hoy.
                  </p>
                </div>
              </div>

              <div className="border-t border-[#F0E8DA] pt-6 flex gap-4 items-start">
                <div className="w-10 h-10 rounded-full bg-[#FAF3E0] flex items-center justify-center shrink-0 border border-[#E8DFC8]">
                  <Truck className="w-5 h-5 text-[#8C533E]" />
                </div>
                <div>
                  <h3 className="font-serif font-bold text-base text-[#3D2C24]">3. Free Delivery in Khulna City</h3>
                  <p className="mt-1 text-xs sm:text-sm text-[#6E5A4F]">
                    Khulna city-r vitore jekono location-e delivery completely free! Cake khub carefully ebong safe box packaging-e pouchano hoy.
                  </p>
                </div>
              </div>

              <div className="border-t border-[#F0E8DA] pt-6 flex gap-4 items-start">
                <div className="w-10 h-10 rounded-full bg-[#FAF3E0] flex items-center justify-center shrink-0 border border-[#E8DFC8]">
                  <MessageCircle className="w-5 h-5 text-[#8C533E]" />
                </div>
                <div>
                  <h3 className="font-serif font-bold text-base text-[#3D2C24]">4. Order Timing & Advance Booking</h3>
                  <p className="mt-1 text-xs sm:text-sm text-[#6E5A4F]">
                    Cake-er fresh baking ebong perfect finish-er jonno minimum 4 to 6 ghonta age order confirm korte hobe. Custom design-er jonno 1 din age janale bhalo hoy.
                  </p>
                </div>
              </div>

            </div>
          </div>
        )}

        {/* ========================================================= */}
        {/* PAGE 4: CONTACT PAGE */}
        {/* ========================================================= */}
        {activeTab === 'contact' && (
          <div className="py-12 max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <div className="text-center mb-10">
              <h2 className="text-3xl font-serif font-bold text-[#4A2E20]">Amader Sathe Contact Korun</h2>
              <div className="w-16 h-1 bg-[#8C533E] mx-auto my-3 rounded-full"></div>
              <p className="text-sm text-[#6E5A4F]">
                Order confirm korte ba jekono proshne amader direct message korun.
              </p>
            </div>

            <div className="grid grid-cols-1 md:grid-cols-2 gap-8">
              
              {/* WhatsApp Box */}
              <div className="bg-white p-8 rounded-2xl border border-[#E8DFC8] shadow-sm text-center flex flex-col items-center justify-between space-y-4">
                <div className="w-14 h-14 bg-[#E8F8EE] rounded-full flex items-center justify-center text-[#25D366]">
                  <MessageCircle className="w-8 h-8" />
                </div>
                <div>
                  <h3 className="font-serif font-bold text-xl text-[#3D2C24]">WhatsApp Direct Order</h3>
                  <p className="text-xs text-[#6E5A4F] mt-1">
                    Direct WhatsApp-e knock korun ebong cake photo soho message din.
                  </p>
                </div>
                <a 
                  href={`https://wa.me/${whatsappNumber}`}
                  target="_blank"
                  rel="noreferrer"
                  className="w-full bg-[#25D366] hover:bg-[#20bd5a] text-white py-3 rounded-xl font-bold text-sm flex items-center justify-center gap-2 shadow-sm transition-all"
                >
                  <MessageCircle className="w-4 h-4" />
                  Chat on WhatsApp
                </a>
              </div>

              {/* Messenger Box */}
              <div className="bg-white p-8 rounded-2xl border border-[#E8DFC8] shadow-sm text-center flex flex-col items-center justify-between space-y-4">
                <div className="w-14 h-14 bg-[#E6F2FF] rounded-full flex items-center justify-center text-[#0084FF]">
                  <Send className="w-8 h-8" />
                </div>
                <div>
                  <h3 className="font-serif font-bold text-xl text-[#3D2C24]">Facebook Messenger</h3>
                  <p className="text-xs text-[#6E5A4F] mt-1">
                    Amader official Facebook page-e message pathate parben.
                  </p>
                </div>
                <a 
                  href={messengerUrl}
                  target="_blank"
                  rel="noreferrer"
                  className="w-full bg-[#0084FF] hover:bg-[#0074e0] text-white py-3 rounded-xl font-bold text-sm flex items-center justify-center gap-2 shadow-sm transition-all"
                >
                  <Send className="w-4 h-4" />
                  Open Messenger
                </a>
              </div>

            </div>
          </div>
        )}

      </main>

      {/* DYNAMIC ORDER MODAL */}
      {orderModalCake && (
        <div className="fixed inset-0 z-50 bg-black/60 backdrop-blur-sm flex items-center justify-center p-4 animate-fadeIn">
          <div className="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl border border-[#E8DFC8] relative space-y-4">
            <button 
              onClick={() => setOrderModalCake(null)}
              className="absolute top-4 right-4 text-gray-400 hover:text-gray-600 p-1"
            >
              <X className="w-5 h-5" />
            </button>

            <div className="text-center">
              <span className="text-xs font-bold text-[#8C533E] uppercase tracking-wider">Confirm Your Order</span>
              <h3 className="text-xl font-serif font-bold text-[#3D2C24]">{orderModalCake.name}</h3>
              <p className="text-xs text-[#6E5A4F] mt-1">Weight: <strong>2 Pounds</strong> | Price: <strong>à§³{orderModalCake.price}</strong></p>
            </div>

            <div className="space-y-3 pt-2">
              <div>
                <label className="block text-xs font-semibold text-[#5C4336] mb-1">Select Cake Shape:</label>
                <select 
                  defaultValue={orderModalCake.shape}
                  id="shapeSelect"
                  className="w-full text-xs p-2.5 rounded-lg border border-[#DCD1BA] bg-[#FAF7F2] text-[#3D2C24] focus:outline-none focus:ring-1 focus:ring-[#8C533E]"
                >
                  <option value="Round">Round Shape</option>
                  <option value="Love">Love Shape (Heart)</option>
                  <option value="Square">Square Shape</option>
                </select>
              </div>

              <div>
                <label className="block text-xs font-semibold text-[#5C4336] mb-1">Custom Message / Delivery Notes:</label>
                <textarea 
                  rows="2"
                  value={customNotes}
                  onChange={(e) => setCustomNotes(e.target.value)}
                  placeholder="Example: Write 'Happy Birthday Tanjil' on cake, Delivery location: Mujgunni, Khulna."
                  className="w-full text-xs p-2.5 rounded-lg border border-[#DCD1BA] bg-[#FAF7F2] text-[#3D2C24] focus:outline-none focus:ring-1 focus:ring-[#8C533E]"
                ></textarea>
              </div>

              <div className="bg-[#FAF3E0] p-3 rounded-lg border border-[#E8DFC8] text-[11px] text-[#5C4336] space-y-1">
                <p>â€¢ <strong>Delivery:</strong> Free delivery all of Khulna city.</p>
                <p>â€¢ <strong>Freshness:</strong> Baked fresh after order confirmation.</p>
              </div>
            </div>

            {/* Modal Actions */}
            <div className="pt-2 flex flex-col gap-2">
              <a 
                href={getWhatsAppLink(
                  orderModalCake, 
                  document.getElementById('shapeSelect')?.value || orderModalCake.shape,
                  customNotes
                )}
                target="_blank"
                rel="noreferrer"
                className="w-full bg-[#25D366] hover:bg-[#20bd5a] text-white py-3 rounded-xl font-bold text-xs flex items-center justify-center gap-2 shadow-sm transition-all"
              >
                <MessageCircle className="w-4 h-4" />
                Send Order to WhatsApp
              </a>
              <a 
                href={messengerUrl}
                target="_blank"
                rel="noreferrer"
                className="w-full bg-[#0084FF] hover:bg-[#0074e0] text-white py-3 rounded-xl font-bold text-xs flex items-center justify-center gap-2 shadow-sm transition-all text-center"
              >
                <Send className="w-4 h-4" />
                Contact via Facebook Messenger
              </a>
            </div>
          </div>
        </div>
      )}

      {/* FOOTER */}
      <footer className="bg-[#3D2C24] text-[#F3EAD8] pt-12 pb-8 border-t border-[#4A2E20]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 md:grid-cols-3 gap-8 mb-8">
          
          <div className="space-y-3">
            <h3 className="font-serif font-bold text-xl text-white">Yummy Cake</h3>
            <p className="text-xs text-[#C5B4A5] leading-relaxed">
              We Care About Every Bite. Pure ingredients, real taste, homemade always. High quality fresh cakes in Khulna City.
            </p>
          </div>

          <div className="space-y-2 text-xs">
            <h4 className="font-bold text-white uppercase tracking-wider">Quick Policies</h4>
            <p className="text-[#C5B4A5]">â€¢ Minimum Order: 2 Pounds</p>
            <p className="text-[#C5B4A5]">â€¢ Delivery: Free all over Khulna City</p>
            <p className="text-[#C5B4A5]">â€¢ Baking: Pure fresh baking on order</p>
          </div>

          <div className="space-y-3">
            <h4 className="font-bold text-xs text-white uppercase tracking-wider">Order Now</h4>
            <div className="flex gap-3">
              <a 
                href={`https://wa.me/${whatsappNumber}`}
                target="_blank"
                rel="noreferrer"
                className="bg-[#25D366] text-white p-2.5 rounded-full hover:opacity-90 transition-opacity"
              >
                <MessageCircle className="w-4 h-4" />
              </a>
              <a 
                href={messengerUrl}
                target="_blank"
                rel="noreferrer"
                className="bg-[#0084FF] text-white p-2.5 rounded-full hover:opacity-90 transition-opacity"
              >
                <Send className="w-4 h-4" />
              </a>
            </div>
          </div>

        </div>

        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 border-t border-white/10 pt-6 text-center text-[11px] text-[#A89485]">
          Â© {new Date().getFullYear()} Yummy Cake Khulna. All rights reserved. Homemade with love.
        </div>
      </footer>

      {/* FLOATING QUICK WHATSAPP BUTTON */}
      <a 
        href={`https://wa.me/${whatsappNumber}`}
        target="_blank"
        rel="noreferrer"
        className="fixed bottom-6 right-6 z-40 bg-[#25D366] text-white p-4 rounded-full shadow-2xl hover:scale-110 transition-transform flex items-center justify-center group"
        title="Chat on WhatsApp"
      >
        <MessageCircle className="w-6 h-6" />
        <span className="max-w-0 overflow-hidden group-hover:max-w-xs transition-all duration-300 whitespace-nowrap text-xs font-bold pl-0 group-hover:pl-2">
          Order Now
        </span>
      </a>

    </div>
  );
}
