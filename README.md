# SMMC
import React, { useState, useEffect } from 'react';
import { Menu, X, Moon, Sun, Globe, ChevronRight } from 'lucide-react';

// --- i18n Data Dictionary ---
const i18n = {
  en: {
    appTitle: "Delta Electronics: Industrial Automation",
    menu: "Menu",
    course: "Strategic Management of MNCs - EMI",
    sections: {
      TP0: "TP0: Company Overview",
      TP1: "TP1: Macro & Industry Analysis",
      TP2: "TP2: Resources & Capabilities",
      TP3: "TP3: Growth & Corporate Strategy"
    },
    placeholders: {
      TP0: "Placeholder for TP0: Recent News, Key Milestones, Vision/Mission/Values, Org Structure, Product Portfolios, and Financial Performance (2019-2023).",
      TP1: "Placeholder for TP1: PESTEL Analysis, Industry Value Chain, Competitor Analysis, Five Forces, and Industry Lifecycle.",
      TP2: "Placeholder for TP2: Core Businesses, Corporate Value Chain, Key Resources (VRIN), Core Competencies, and Dynamic Capabilities.",
      TP3: "Placeholder for TP3: Vertical Integration, Diversification, Geographical Expansion, Entry Modes (M&A, JV), and Future Challenges."
    },
    footerLeft: "SPA Version 1.0.0 | © 2026 SMMC Group.",
    footerRight: "Advisor: Prof. Shihmin Lo | Members: [ID] [Eng Name] / [中文名]"
  },
  zh: {
    appTitle: "台達電子：工業自動化事業群策略分析",
    menu: "選單",
    course: "跨國企業策略管理 (SMMC)",
    sections: {
      TP0: "TP0: 企業總覽與財務績效",
      TP1: "TP1: 總體環境與產業分析",
      TP2: "TP2: 企業資源與核心能耐",
      TP3: "TP3: 成長策略與未來挑戰"
    },
    placeholders: {
      TP0: "TP0 內容保留區：最新新聞、重要里程碑、願景/使命/價值觀、組織架構、產品組合與 2019-2023 財務表現。",
      TP1: "TP1 內容保留區：PESTEL 分析、產業價值鏈、競爭者分析、五力分析與產業生命週期。",
      TP2: "TP2 內容保留區：核心事業、企業價值鏈、關鍵資源 (VRIN)、核心能耐與動態能力。",
      TP3: "TP3 內容保留區：垂直整合、多角化、地理擴張、進入模式（併購、合資）與未來挑戰及建議。"
    },
    footerLeft: "SPA 版本 1.0.0 | © 2026 SMMC 報告小組.",
    footerRight: "指導教授: 羅世民 博士 | 組員: [學號] [中文名] / [Eng Name]"
  }
};

export default function App() {
  const [lang, setLang] = useState('en');
  const [isDarkMode, setIsDarkMode] = useState(false);
  const [activeTab, setActiveTab] = useState('TP0');
  const [isMenuOpen, setIsMenuOpen] = useState(false);

  const t = i18n[lang];

  // Toggle Dark Mode globally
  useEffect(() => {
    if (isDarkMode) {
      document.documentElement.classList.add('dark');
    } else {
      document.documentElement.classList.remove('dark');
    }
  }, [isDarkMode]);

  const toggleLang = () => {
    setLang(lang === 'en' ? 'zh' : 'en');
  };

  const handleTabChange = (tab) => {
    setActiveTab(tab);
    setIsMenuOpen(false); // Close menu on mobile after clicking
  };

  return (
    <div className={`min-h-screen flex flex-col font-sans transition-colors duration-300 ${isDarkMode ? 'bg-gray-900 text-gray-100' : 'bg-gray-50 text-gray-800'}`}>
      
      {/* Header */}
      <header className={`sticky top-0 z-40 w-full shadow-md transition-colors duration-300 ${isDarkMode ? 'bg-gray-800 border-b border-gray-700' : 'bg-white border-b border-gray-200'}`}>
        <div className="flex items-center justify-between px-4 h-16 max-w-7xl mx-auto">
          
          {/* Header Left: Menu Button & Title */}
          <div className="flex items-center space-x-4">
            <button 
              onClick={() => setIsMenuOpen(!isMenuOpen)}
              className={`p-2 rounded-sm focus:outline-none focus:ring-2 focus:ring-[#005A9C] ${isDarkMode ? 'hover:bg-gray-700' : 'hover:bg-gray-100'}`}
              aria-label={t.menu}
            >
              {isMenuOpen ? <X size={24} className="text-[#005A9C]" /> : <Menu size={24} className="text-[#005A9C]" />}
            </button>
            <div className="flex flex-col">
              <span className={`text-xs font-bold uppercase tracking-wider ${isDarkMode ? 'text-gray-400' : 'text-gray-500'}`}>
                {t.course}
              </span>
              <h1 className={`text-lg md:text-xl font-extrabold ${isDarkMode ? 'text-white' : 'text-[#005A9C]'}`}>
                {t.appTitle}
              </h1>
            </div>
          </div>

          {/* Header Right: Language & Theme Toggles */}
          <div className="flex items-center space-x-1 md:space-x-3">
            <button 
              onClick={toggleLang}
              className={`flex items-center space-x-1 p-2 rounded-sm text-sm font-medium transition-colors ${isDarkMode ? 'hover:bg-gray-700' : 'hover:bg-gray-100'}`}
              title="Toggle Language"
            >
              <Globe size={20} className="text-[#005A9C]" />
              <span className="hidden md:inline">{lang === 'en' ? '中文' : 'EN'}</span>
            </button>
            <button 
              onClick={() => setIsDarkMode(!isDarkMode)}
              className={`p-2 rounded-sm transition-colors ${isDarkMode ? 'hover:bg-gray-700 text-yellow-400' : 'hover:bg-gray-100 text-gray-600'}`}
              title="Toggle Dark/Light Mode"
            >
              {isDarkMode ? <Sun size={20} /> : <Moon size={20} />}
            </button>
          </div>
        </div>
      </header>

      {/* Main Layout */}
      <div className="flex-1 flex max-w-7xl w-full mx-auto relative overflow-hidden">
        
        {/* Sidebar Navigation (Responsive) */}
        <aside 
          className={`absolute md:relative z-30 w-64 h-full transform transition-transform duration-300 ease-in-out border-r ${
            isMenuOpen ? 'translate-x-0' : '-translate-x-full md:translate-x-0'
          } ${isDarkMode ? 'bg-gray-800 border-gray-700' : 'bg-white border-gray-200'}`}
        >
          <nav className="p-4 space-y-2 mt-2">
            {Object.entries(t.sections).map(([key, label]) => (
              <button
                key={key}
                onClick={() => handleTabChange(key)}
                className={`w-full flex items-center justify-between text-left px-4 py-3 rounded-sm transition-all duration-200 ${
                  activeTab === key 
                    ? 'bg-[#005A9C] text-white shadow-md' 
                    : `${isDarkMode ? 'text-gray-300 hover:bg-gray-700' : 'text-gray-700 hover:bg-gray-100'}`
                }`}
              >
                <span className="font-semibold text-sm">{label}</span>
                {activeTab === key && <ChevronRight size={16} />}
              </button>
            ))}
          </nav>
        </aside>

        {/* Mobile overlay for sidebar */}
        {isMenuOpen && (
          <div 
            className="absolute inset-0 bg-black/50 z-20 md:hidden" 
            onClick={() => setIsMenuOpen(false)}
          />
        )}

        {/* Content Area */}
        <main className="flex-1 p-6 md:p-10 overflow-y-auto">
          <div className={`max-w-4xl mx-auto rounded-sm border p-8 shadow-sm transition-colors duration-300 ${
            isDarkMode ? 'bg-gray-800 border-gray-700' : 'bg-white border-gray-200'
          }`}>
            
            <div className="border-b-2 border-[#005A9C] pb-4 mb-6">
              <h2 className="text-2xl md:text-3xl font-bold tracking-tight">
                {t.sections[activeTab]}
              </h2>
            </div>
            
            <div className={`min-h-[400px] flex items-center justify-center p-6 border-2 border-dashed rounded-sm ${
              isDarkMode ? 'border-gray-600 text-gray-400 bg-gray-900/50' : 'border-gray-300 text-gray-500 bg-gray-50'
            }`}>
              <p className="text-center text-lg leading-relaxed max-w-2xl">
                {t.placeholders[activeTab]}
              </p>
            </div>
            
            {/* Action buttons placeholder for future development */}
            <div className="mt-8 flex justify-end">
              <button className="px-6 py-2 bg-[#005A9C] text-white text-sm font-semibold rounded-sm hover:bg-blue-800 transition-colors shadow-sm">
                {lang === 'en' ? 'Edit Content' : '編輯內容'}
              </button>
            </div>

          </div>
        </main>
      </div>

      {/* Footer */}
      <footer className={`w-full py-4 px-6 border-t transition-colors duration-300 ${
        isDarkMode ? 'bg-gray-800 border-gray-700 text-gray-400' : 'bg-white border-gray-200 text-gray-500'
      }`}>
        <div className="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center text-xs space-y-2 md:space-y-0">
          <div className="text-center md:text-left">
            {t.footerLeft}
          </div>
          <div className="text-center md:text-right font-medium">
            {t.footerRight}
          </div>
        </div>
      </footer>

    </div>
  );
}
