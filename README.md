/*
Multi-page Company Website (React + Tailwind)
File: App.jsx (single-file demo)
Purpose: Full multi-page sample for BROS E&C JSC with VI/EN support, routes, pages: Home, About, Services, Projects, News, Contact.
How to use:
1. Create a React app (Vite or CRA). Install dependencies: framer-motion, react-router-dom, tailwindcss (and configure Tailwind).
   npm install react-router-dom framer-motion
2. Put this file in src/App.jsx and place your logo at public/logo.jpeg.
3. Start dev server: npm run dev (Vite) or npm start (CRA).

Customization: replace texts, images, add API, connect contact form.
*/

import React, { useState, createContext, useContext } from 'react'
import { BrowserRouter as Router, Routes, Route, Link, useNavigate } from 'react-router-dom'
import { motion } from 'framer-motion'

// Language context
const LangContext = createContext()
const useLang = () => useContext(LangContext)

const translations = {
  vi: {
    home: 'Trang chủ', about: 'Giới thiệu', services: 'Dịch vụ', projects: 'Dự án', news: 'Tin tức', contact: 'Liên hệ',
    slogan: 'The art of professionalism', quoteBtn: 'Yêu cầu báo giá', viewProjects: 'Xem dự án', quickQuote: 'Nhận báo giá nhanh',
    phone: 'Điện thoại', address: 'Địa chỉ', email: 'Email',
    aboutTitle: 'Về chúng tôi', servicesTitle: 'Các dịch vụ của chúng tôi', projectsTitle: 'Dự án tiêu biểu', newsTitle: 'Tin tức & Sự kiện', contactTitle: 'Liên hệ'
  },
  en: {
    home: 'Home', about: 'About', services: 'Services', projects: 'Projects', news: 'News', contact: 'Contact',
    slogan: 'The art of professionalism', quoteBtn: 'Request a Quote', viewProjects: 'View Projects', quickQuote: 'Quick Quote',
    phone: 'Phone', address: 'Address', email: 'Email',
    aboutTitle: 'About Us', servicesTitle: 'Our Services', projectsTitle: 'Featured Projects', newsTitle: 'News & Events', contactTitle: 'Contact'
  }
}

const Nav = () => {
  const {lang, setLang, t} = useLang()
  return (
    <header className="bg-black text-white">
      <div className="max-w-6xl mx-auto px-6 py-4 flex items-center justify-between">
        <div className="flex items-center gap-4">
          <div className="w-12 h-12 bg-white rounded flex items-center justify-center overflow-hidden">
            <img src="/logo.jpeg" alt="logo" className="object-contain" />
          </div>
          <div>
            <div className="font-semibold">BROS E&C JSC</div>
            <div className="text-sm text-orange-400">{t.slogan}</div>
          </div>
        </div>

        <nav className="hidden md:flex gap-6 text-sm">
          <Link to="/">{t.home}</Link>
          <Link to="/about">{t.about}</Link>
          <Link to="/services">{t.services}</Link>
          <Link to="/projects">{t.projects}</Link>
          <Link to="/news">{t.news}</Link>
          <Link to="/contact">{t.contact}</Link>
        </nav>

        <div className="flex items-center gap-3">
          <button onClick={() => setLang('vi')} className={`px-2 py-1 rounded ${lang==='vi'?'bg-orange-500 text-white':'bg-white text-black'}`}>VI</button>
          <button onClick={() => setLang('en')} className={`px-2 py-1 rounded ${lang==='en'?'bg-orange-500 text-white':'bg-white text-black'}`}>EN</button>
        </div>
      </div>
    </header>
  )
}

const Home = () => {
  const {t} = useLang()
  const navigate = useNavigate()
  return (
    <main className="max-w-6xl mx-auto px-6 py-12">
      <section className="grid md:grid-cols-2 gap-8 items-center">
        <motion.div initial={{ x: -20, opacity: 0 }} animate={{ x:0, opacity:1 }} transition={{duration:0.4}}>
          <h1 className="text-3xl md:text-4xl font-extrabold text-black">BROS E&C JSC</h1>
          <p className="mt-4 text-gray-700 text-lg">{t.slogan}</p>
          <div className="mt-6 flex gap-3">
            <button onClick={() => navigate('/contact')} className="px-5 py-3 bg-orange-500 text-white rounded">{t.quoteBtn}</button>
            <button onClick={() => navigate('/projects')} className="px-5 py-3 border border-orange-500 text-orange-500 rounded">{t.viewProjects}</button>
          </div>
        </motion.div>

        <motion.div initial={{ scale: 0.98, opacity:0 }} animate={{ scale:1, opacity:1 }} transition={{duration:0.5}} className="rounded-lg bg-gray-50 border border-gray-200 p-6">
          <h3 className="font-semibold">{t.quickQuote}</h3>
          <QuickQuoteForm />
        </motion.div>
      </section>

      <section className="mt-12">
        <h2 className="text-2xl font-bold">{t.servicesTitle}</h2>
        <ServicesGrid />
      </section>

      <section className="mt-12">
        <h2 className="text-2xl font-bold">{t.projectsTitle}</h2>
        <ProjectsPreview />
      </section>
    </main>
  )
}

const About = () => {
  const {t} = useLang()
  return (
    <div className="max-w-6xl mx-auto px-6 py-12">
      <h2 className="text-2xl font-bold">{t.aboutTitle}</h2>
      <p className="mt-4 text-gray-700">BROS E&C là nhà thầu xây dựng, thiết kế và cải tạo, cam kết mang đến giải pháp chuyên nghiệp, sáng tạo và hiệu quả cho mọi công trình. (Bạn có thể thay đổi phần này thành lịch sử công ty, tầm nhìn, đội ngũ...)</p>
    </div>
  )
}

const Services = () => {
  const {t} = useLang()
  return (
    <div className="max-w-6xl mx-auto px-6 py-12">
      <h2 className="text-2xl font-bold">{t.servicesTitle}</h2>
      <div className="mt-6 grid md:grid-cols-3 gap-6">
        <ServiceCard titleKey={{vi:'Nhà thầu xây dựng', en:'General Contractor'}} descKey={{vi:'Thi công trọn gói công trình dân dụng và công nghiệp.', en:'Turnkey construction for civil and industrial projects.'}} />
        <ServiceCard titleKey={{vi:'Thiết kế', en:'Design'}} descKey={{vi:'Thiết kế kiến trúc & kết cấu', en:'Architectural & structural design services.'}} />
        <ServiceCard titleKey={{vi:'Cải tạo', en:'Renovation'}} descKey={{vi:'Cải tạo, nâng cấp công trình hiện hữu.', en:'Renovation and upgrading of existing buildings.'}} />
      </div>
    </div>
  )
}

const Projects = () => {
  const {t} = useLang()
  const sample = [
    {id:1, title:{vi:'Công trình A', en:'Project A'}, desc:{vi:'Mô tả dự án A', en:'Description A'}},
    {id:2, title:{vi:'Công trình B', en:'Project B'}, desc:{vi:'Mô tả dự án B', en:'Description B'}},
    {id:3, title:{vi:'Công trình C', en:'Project C'}, desc:{vi:'Mô tả dự án C', en:'Description C'}},
  ]
  const {lang} = useLang()
  return (
    <div className="max-w-6xl mx-auto px-6 py-12">
      <h2 className="text-2xl font-bold">{t.projectsTitle}</h2>
      <div className="mt-6 grid md:grid-cols-3 gap-6">
        {sample.map(p => (
          <div key={p.id} className="bg-white rounded shadow border border-gray-200 overflow-hidden">
            <div className="h-40 bg-gray-200 flex items-center justify-center">Image</div>
            <div className="p-4">
              <h4 className="font-semibold">{p.title[lang]}</h4>
              <p className="text-sm text-gray-600 mt-2">{p.desc[lang]}</p>
            </div>
          </div>
        ))}
      </div>
    </div>
  )
}

const News = () => {
  const {t} = useLang()
  const {lang} = useLang()
  const items = [
    {id:1, title:{vi:'Tin 1', en:'News 1'}, excerpt:{vi:'Tóm tắt tin 1', en:'Excerpt 1'}},
    {id:2, title:{vi:'Tin 2', en:'News 2'}, excerpt:{vi:'Tóm tắt tin 2', en:'Excerpt 2'}},
  ]
  return (
    <div className="max-w-6xl mx-auto px-6 py-12">
      <h2 className="text-2xl font-bold">{t.newsTitle}</h2>
      <div className="mt-6 space-y-4">
        {items.map(i => (
          <div key={i.id} className="p-4 border rounded bg-white">
            <h4 className="font-semibold">{i.title[lang]}</h4>
            <p className="text-sm text-gray-600 mt-2">{i.excerpt[lang]}</p>
          </div>
        ))}
      </div>
    </div>
  )
}

const Contact = () => {
  const {t} = useLang()
  return (
    <div className="max-w-6xl mx-auto px-6 py-12 grid md:grid-cols-2 gap-8">
      <div className="bg-gray-50 p-6 rounded border border-gray-200">
        <h3 className="font-bold text-lg">{t.contactTitle}</h3>
        <ul className="mt-4 text-sm space-y-2">
          <li><strong>{t.phone}:</strong> 0123 456 789</li>
          <li><strong>{t.email}:</strong> info@brosec.vn</li>
          <li><strong>{t.address}:</strong> Hanoi, Vietnam</li>
        </ul>
      </div>
      <div className="bg-gray-50 p-6 rounded border border-gray-200">
        <h3 className="font-bold text-lg">{t.contactTitle}</h3>
        <ContactForm />
      </div>
    </div>
  )
}

// small components
const ServiceCard = ({titleKey, descKey}) => {
  const {lang} = useLang()
  return (
    <div className="bg-white p-5 rounded shadow border border-gray-200">
      <h3 className="font-semibold text-orange-500">{titleKey[lang]}</h3>
      <p className="mt-2 text-gray-600 text-sm">{descKey[lang]}</p>
    </div>
  )
}

const ServicesGrid = () => {
  const {lang} = useLang()
  const s = [
    {id:1, title:{vi:'Nhà thầu xây dựng', en:'General Contractor'}, desc:{vi:'Thi công trọn gói', en:'Turnkey construction'}},
    {id:2, title:{vi:'Thiết kế', en:'Design'}, desc:{vi:'Thiết kế kiến trúc & kết cấu', en:'Architectural & structural design'}},
    {id:3, title:{vi:'Cải tạo', en:'Renovation'}, desc:{vi:'Cải tạo, nâng cấp', en:'Renovation & upgrading'}},
  ]
  return (
    <div className="mt-6 grid md:grid-cols-3 gap-6">
      {s.map(x => (
        <div key={x.id} className="bg-white p-5 rounded shadow border border-gray-200">
          <h4 className="font-semibold text-orange-500">{x.title[lang]}</h4>
          <p className="mt-2 text-gray-600 text-sm">{x.desc[lang]}</p>
        </div>
      ))}
    </div>
  )
}

const ProjectsPreview = () => {
  const {lang} = useLang()
  return (
    <div className="mt-6 grid md:grid-cols-3 gap-6">
      {[1,2,3].map(i => (
        <div key={i} className="bg-white rounded shadow border border-gray-200 overflow-hidden">
          <div className="h-40 bg-gray-200 flex items-center justify-center">Image</div>
          <div className="p-4">
            <h4 className="font-semibold">{lang==='vi'?`Tên dự án ${i}`:`Project ${i}`}</h4>
            <p className="text-sm text-gray-600 mt-2">{lang==='vi'?`Mô tả ngắn dự án ${i}`:`Brief description ${i}`}</p>
          </div>
        </div>
      ))}
    </div>
  )
}

const QuickQuoteForm = () => {
  const {lang} = useLang()
  return (
    <form className="mt-4 grid gap-3">
      <input placeholder={lang==='vi'?'Họ tên':'Full name'} className="border p-2 rounded" />
      <input placeholder={lang==='vi'?'Số điện thoại':'Phone'} className="border p-2 rounded" />
      <input placeholder="Email" className="border p-2 rounded" />
      <textarea placeholder={lang==='vi'?'Mô tả yêu cầu':'Project details'} className="border p-2 rounded" rows={3} />
      <button type="button" className="px-4 py-2 bg-orange-500 text-white rounded">{lang==='vi'?'Gửi':'Send'}</button>
    </form>
  )
}

const ContactForm = () => {
  const {lang} = useLang()
  return (
    <form className="grid gap-3">
      <input placeholder={lang==='vi'?'Họ tên':'Full name'} className="border p-2 rounded" />
      <input placeholder={lang==='vi'?'Số điện thoại':'Phone'} className="border p-2 rounded" />
      <input placeholder="Email" className="border p-2 rounded" />
      <textarea placeholder={lang==='vi'?'Nội dung':'Message'} className="border p-2 rounded" rows={4} />
      <button type="button" className="px-4 py-2 bg-orange-500 text-white rounded">{lang==='vi'?'Gửi':'Send'}</button>
    </form>
  )
}

export default function App() {
  const [lang, setLang] = useState('vi')
  const t = translations[lang]

  return (
    <LangContext.Provider value={{lang, setLang, t}}>
      <Router>
        <div className="min-h-screen bg-white text-gray-800 flex flex-col">
          <Nav />

          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/services" element={<Services />} />
            <Route path="/projects" element={<Projects />} />
            <Route path="/news" element={<News />} />
            <Route path="/contact" element={<Contact />} />
          </Routes>

          <footer className="bg-black text-white mt-auto">
            <div className="max-w-6xl mx-auto px-6 py-6 flex flex-col md:flex-row justify-between items-center gap-4 text-sm">
              <div>© {new Date().getFullYear()} BROS E&C JSC. All rights reserved.</div>
              <div className="flex gap-4">
                <a href="#">Policy</a>
                <a href="#">Terms</a>
              </div>
            </div>
          </footer>
        </div>
      </Router>
    </LangContext.Provider>
  )
}
