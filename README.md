<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KiotViet - Code of Conduct Hub</title>
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        @keyframes moveInCircle   { 0%{transform:rotate(0deg)} 50%{transform:rotate(180deg)} 100%{transform:rotate(360deg)} }
        @keyframes moveVertical   { 0%{transform:translateY(-50%)} 50%{transform:translateY(50%)} 100%{transform:translateY(-50%)} }
        @keyframes moveHorizontal { 0%{transform:translateX(-50%)} 50%{transform:translateX(50%)} 100%{transform:translateX(-50%)} }
        @keyframes fadeUp   { from{opacity:0;transform:translateY(20px)} to{opacity:1;transform:translateY(0)} }
        @keyframes fadeIn   { from{opacity:0} to{opacity:1} }
        @keyframes scaleIn  { from{opacity:0;transform:scale(0.97) translateY(10px)} to{opacity:1;transform:scale(1) translateY(0)} }
        @keyframes slideDown{ from{opacity:0;transform:translateY(-6px)} to{opacity:1;transform:translateY(0)} }
        .animate-fade-up  { animation: fadeUp 0.6s ease-out forwards; }
        .animate-scale-in { animation: scaleIn 0.35s cubic-bezier(0.34,1.56,0.64,1) forwards; }
        .delay-100 { animation-delay: 0.1s; }
        .soft-glow-background { position:fixed;top:0;left:0;width:100%;height:100%;z-index:-10;background:linear-gradient(to bottom right,#f8fafc,#e0f2fe); }
        .shape  { position:absolute;filter:blur(140px);opacity:0.4; }
        .shape1 { height:350px;width:350px;background:#3b82f6;border-radius:50%;top:-50px;left:-100px;animation:moveInCircle 22s ease-in-out infinite; }
        .shape2 { height:450px;width:450px;background:#22c55e;border-radius:50%;bottom:-100px;right:-100px;animation:moveVertical 28s ease-in-out infinite; }
        .shape3 { height:300px;width:500px;background:#f97316;border-radius:50%;top:50%;left:50%;animation:moveHorizontal 35s ease-in-out infinite; }

        /* Kinh Doanh styles */
        .section-card { display:flex;align-items:center;justify-content:space-between;padding:20px 24px;background:white;border-radius:16px;border:1px solid #e2e8f0;box-shadow:0 2px 8px rgba(0,0,0,0.05);cursor:pointer;transition:transform .25s cubic-bezier(.34,1.56,.64,1),box-shadow .25s ease,border-color .25s ease,background .25s ease; }
        .section-card:hover { transform:translateY(-3px);box-shadow:0 14px 36px rgba(59,130,246,0.14),0 4px 12px rgba(0,0,0,0.07);border-color:#93c5fd;background:linear-gradient(to right,#fafcff,#f0f4ff); }
        .kd-arrow-btn { display:flex;align-items:center;justify-content:center;width:36px;height:36px;border-radius:50%;background:#f1f5f9;color:#94a3b8;flex-shrink:0;transition:background .2s ease,color .2s ease,transform .35s cubic-bezier(.34,1.56,.64,1); }
        .section-card:hover .kd-arrow-btn { background:#dbeafe;color:#3b82f6;transform:rotate(90deg); }
        .doc-count { display:inline-flex;align-items:center;gap:5px;font-size:12px;font-weight:600;color:#475569;background:#f8fafc;padding:4px 12px;border-radius:999px;border:1px solid #e2e8f0;white-space:nowrap;opacity:0;transform:translateX(-10px);transition:opacity .22s ease,transform .25s cubic-bezier(.34,1.56,.64,1); }
        .section-card:hover .doc-count { opacity:1;transform:translateX(0); }
        .item-row, .focus-row { display:flex;align-items:center;justify-content:space-between;padding:14px 18px;border-radius:14px;cursor:pointer;background:white;border:1px solid #e2e8f0;box-shadow:0 1px 4px rgba(0,0,0,0.05);transition:all .22s cubic-bezier(.34,1.56,.64,1);text-decoration:none; }
        .item-row:hover, .focus-row:hover { background:linear-gradient(to right,#eff6ff,#eef2ff);border-color:#93c5fd;box-shadow:0 6px 20px rgba(59,130,246,0.12);transform:translateY(-2px); }
        .chev-spin { transition:transform .3s cubic-bezier(.34,1.56,.64,1); }
        .item-row:hover .chev-spin, .focus-row:hover .chev-spin { transform:rotate(90deg); }
        .spotlight-overlay { position:fixed;inset:0;z-index:40;background:rgba(15,23,42,0.6);backdrop-filter:blur(4px);animation:fadeIn .25s ease-out; }
        .reg-icon-0{background:#eff6ff;color:#3b82f6} .reg-icon-1{background:#f0fdf4;color:#22c55e} .reg-icon-2{background:#faf5ff;color:#a855f7} .reg-icon-3{background:#fff7ed;color:#f97316}
    </style>
</head>
<body class="text-slate-700 bg-slate-50 antialiased overflow-x-hidden selection:bg-blue-100 selection:text-blue-900">
<div id="root"></div>
<script type="text/babel">
    const { useState, useEffect } = React;

    /* ── Icons ── */
    const IB = ({children, className, ...p}) => (
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
             fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"
             className={className} {...p}>{children}</svg>
    );
    const Shield      = p => <IB {...p}><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></IB>;
    const Users       = p => <IB {...p}><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></IB>;
    const Headphones  = p => <IB {...p}><path d="M3 18v-6a9 9 0 0 1 18 0v6"/><path d="M21 19a2 2 0 0 1-2 2h-1a2 2 0 0 1-2-2v-3a2 2 0 0 1 2-2h3zM3 19a2 2 0 0 0 2 2h1a2 2 0 0 0 2-2v-3a2 2 0 0 0-2-2H3z"/></IB>;
    const BookOpenIco = p => <IB {...p}><path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/></IB>;
    const FileText    = p => <IB {...p}><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/><polyline points="10 9 9 9 8 9"/></IB>;
    const Info        = p => <IB {...p}><circle cx="12" cy="12" r="10"/><line x1="12" y1="16" x2="12" y2="12"/><line x1="12" y1="8" x2="12.01" y2="8"/></IB>;
    const Search      = p => <IB {...p}><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></IB>;
    const ArrowRight  = p => <IB {...p}><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></IB>;
    const ArrowLeft   = p => <IB {...p}><line x1="19" y1="12" x2="5" y2="12"/><polyline points="12 19 5 12 12 5"/></IB>;
    const ArrowUp     = p => <IB {...p}><line x1="12" y1="19" x2="12" y2="5"/><polyline points="5 12 12 5 19 12"/></IB>;
    const ExtLink     = p => <IB {...p}><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></IB>;
    const ChevRight   = p => <IB {...p}><polyline points="9 18 15 12 9 6"/></IB>;
    const HomeIco     = p => <IB {...p}><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></IB>;
    const DollarSign  = p => <IB {...p}><line x1="12" y1="1" x2="12" y2="23"/><path d="M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"/></IB>;
    const CheckCircle = p => <IB {...p}><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></IB>;
    const FileTextKD  = p => <IB {...p}><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/></IB>;
    const CreditCard  = p => <IB {...p}><rect x="1" y="4" width="22" height="16" rx="2" ry="2"/><line x1="1" y1="10" x2="23" y2="10"/></IB>;
    const SettingsIco = p => <IB {...p}><circle cx="12" cy="12" r="3"/><path d="M12 1v2m0 18v2m11-11h-2M3 12H1"/></IB>;
    const DocIco      = p => <IB {...p}><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></IB>;
    const XIco        = p => <IB {...p}><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></IB>;
    const ClockIco    = p => <IB {...p}><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></IB>;
    const UsersSmall  = p => <IB {...p}><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/></IB>;
    const regIcons = [ClockIco, CheckCircle, UsersSmall, FileTextKD];

    /* ── SHARED ── */
    const BgShapes = () => (
        <div className="soft-glow-background">
            <div className="shape shape1"/><div className="shape shape2"/><div className="shape shape3"/>
        </div>
    );

    const ScrollToTop = () => {
        const [v, setV] = useState(false);
        useEffect(() => {
            const h = () => setV(window.scrollY > 300);
            window.addEventListener('scroll', h);
            return () => window.removeEventListener('scroll', h);
        }, []);
        return v ? (
            <button onClick={() => window.scrollTo({top:0,behavior:'smooth'})}
                className="fixed bottom-8 right-8 bg-blue-600 text-white p-3 rounded-full shadow-xl hover:bg-blue-700 hover:scale-110 transition-all z-50">
                <ArrowUp className="w-5 h-5"/>
            </button>
        ) : null;
    };

    const Footer = () => (
        <footer className="bg-slate-800 text-white pt-12 pb-8 border-t border-slate-700">
            <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
                <div className="flex justify-center mb-6">
                    <img src="https://logo.kiotviet.vn/KiotViet-Logo-Horizontal-White.svg" alt="KiotViet" className="h-8 opacity-90 hover:opacity-100 transition-opacity"/>
                </div>
                <p className="text-slate-200 font-medium text-lg mb-2">Operation Management</p>
                <p className="text-slate-400 text-sm mb-6 max-w-2xl mx-auto">
                    Bản quyền tài liệu thuộc về Công ty Cổ phần Công nghệ KiotViet.<br/>
                    Nghiêm cấm mọi hành vi chia sẻ/phát tán thông tin CoC ngoài phạm vi nội bộ.
                </p>
                <div className="w-16 h-1 bg-blue-500 rounded-full mx-auto mb-6"></div>
                <p className="text-slate-500 text-xs">© {new Date().getFullYear()} KiotViet. Internal Use Only.</p>
            </div>
        </footer>
    );

    /* ══════════════════════════════════════════
       TRANG CHỦ
    ══════════════════════════════════════════ */
    const generalRules = [
        { id:'gr-1', title:"Nội quy lao động", url:"https://drive.google.com/file/d/1nTEpqqRj-nciLtPLMUlTXYqO6tpaj7R1/view?usp=drive_link" },
        { id:'gr-2', title:"Quy định trang phục, đồng phục", url:"https://drive.google.com/file/d/1cVseNT1hJ7xq7K86ywkwxrLe_jrfyhv1/view?usp=drive_link" },
    ];

    const homeDocuments = [
        { id:1, title:"Quy định chung",       description:"Các nguyên tắc ứng xử, quy định nền tảng và văn hóa chung.",        icon:<Shield className="w-6 h-6"/>,    internal:true,  colorClass:"text-blue-600",   bgClass:"bg-blue-50",   hoverBorder:"hover:border-blue-300",   hoverBg:"hover:bg-blue-50"   },
        { id:2, title:"Quy trình - Kinh doanh",description:"Quy định bán hàng, luồng quy trình làm việc cho khối Sales.",        icon:<Users className="w-6 h-6"/>,     internal:true,  colorClass:"text-green-600",  bgClass:"bg-green-50",  hoverBorder:"hover:border-green-300",  hoverBg:"hover:bg-green-50"  },
        { id:3, title:"Quy trình - DVKH",      description:"Quy chuẩn giao tiếp, xử lý khiếu nại và hỗ trợ khách hàng.",       icon:<Headphones className="w-6 h-6"/>,internal:false, url:"https://sites.google.com/kiotviet.com/operation-management/d%E1%BB%8Bch-v%E1%BB%A5-kh%C3%A1ch-h%C3%A0ng", colorClass:"text-purple-600", bgClass:"bg-purple-50", hoverBorder:"hover:border-purple-300", hoverBg:"hover:bg-purple-50" },
        { id:4, title:"Chính sách bán hàng",   description:"Cập nhật các chính sách giá, khuyến mãi và chiết khấu.",            icon:<BookOpenIco className="w-6 h-6"/>,internal:false, url:"https://sites.google.com/kiotviet.com/coc/ch%C3%ADnh-s%C3%A1ch",                                          colorClass:"text-orange-600", bgClass:"bg-orange-50", hoverBorder:"hover:border-orange-300", hoverBg:"hover:bg-orange-50" },
        { id:5, title:"Mẫu hợp đồng",          description:"Kho lưu trữ các biểu mẫu, hợp đồng và phụ lục chuẩn.",             icon:<FileText className="w-6 h-6"/>,  internal:false, url:"https://sites.google.com/kiotviet.com/coc/m%E1%BA%ABu-h%E1%BB%A3p-%C4%91%E1%BB%93ng",                  colorClass:"text-teal-600",   bgClass:"bg-teal-50",   hoverBorder:"hover:border-teal-300",   hoverBg:"hover:bg-teal-50"   },
        { id:6, title:"Hướng dẫn sử dụng",     description:"Tài liệu hướng dẫn thao tác hệ thống CRM và công cụ.",              icon:<Info className="w-6 h-6"/>,      internal:false, url:"https://sites.google.com/kiotviet.com/coc/hdsd/01-hd-hdsd-crm",                                           colorClass:"text-indigo-600", bgClass:"bg-indigo-50", hoverBorder:"hover:border-indigo-300", hoverBg:"hover:bg-indigo-50" },
    ];

    /* ══════════════════════════════════════════
       QUY ĐỊNH CHUNG PAGE
    ══════════════════════════════════════════ */
    const QuyDinhChungPage = ({ onBack }) => {
        const [searchTerm, setSearchTerm] = useState('');
        const filtered = generalRules.filter(r => r.title.toLowerCase().includes(searchTerm.toLowerCase()));
        return (
            <div className="min-h-screen flex flex-col relative">
                <BgShapes/>
                <header className="sticky top-0 z-40 backdrop-blur-md bg-white/80 border-b border-slate-200 shadow-sm">
                    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                        <div className="flex items-center justify-between h-16">
                            <div className="flex items-center gap-3">
                                <button onClick={onBack} className="flex items-center gap-2 px-3 py-1.5 rounded-lg text-slate-600 hover:text-blue-600 hover:bg-blue-50 transition-all font-medium text-sm">
                                    <ArrowLeft className="w-4 h-4"/><span className="hidden sm:inline">Trang chủ</span>
                                </button>
                                <div className="h-4 w-px bg-slate-300 hidden sm:block"></div>
                                <img src="https://logo.kiotviet.vn/KiotViet-Logo-Horizontal.svg" alt="KiotViet" className="h-8"/>
                                <div className="h-4 w-px bg-slate-300 hidden sm:block"></div>
                                <span className="hidden md:inline text-sm font-semibold text-slate-600">Code of Conduct</span>
                            </div>
                            <div className="hidden md:flex relative group">
                                <input type="text" placeholder="Tìm kiếm..." value={searchTerm} onChange={e=>setSearchTerm(e.target.value)}
                                    className="pl-9 pr-4 py-1.5 bg-slate-100/50 border-none rounded-full text-sm focus:ring-2 focus:ring-blue-500/50 transition-all w-48 group-hover:w-64 focus:w-64"/>
                                <span className="absolute left-3 top-2 text-slate-400"><Search className="w-4 h-4"/></span>
                            </div>
                        </div>
                    </div>
                </header>
                <main className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 md:py-16 flex-1">
                    <nav className="flex items-center gap-2 text-sm text-slate-500 mb-10 animate-fade-up">
                        <button onClick={onBack} className="flex items-center gap-1.5 hover:text-blue-600 transition-colors font-medium">
                            <HomeIco className="w-4 h-4"/><span>Trang chủ</span>
                        </button>
                        <ChevRight className="w-4 h-4 text-slate-300"/>
                        <span className="text-slate-800 font-semibold">Quy định chung</span>
                    </nav>
                    <section className="text-center mb-16 animate-fade-up">
                        <h1 className="text-4xl md:text-5xl font-extrabold tracking-tight leading-tight">
                            <span className="text-blue-600">QUY ĐỊNH CHUNG</span>
                        </h1>
                        <p className="mt-4 text-lg text-slate-600 max-w-3xl mx-auto font-medium">
                            Các nguyên tắc ứng xử, quy định nền tảng và văn hóa chung.<br className="hidden md:block"/> CBNV thuộc Công ty Cổ phần Công nghệ KiotViet
                        </p>
                        <div className="md:hidden mt-8 relative max-w-sm mx-auto">
                            <input type="text" placeholder="Tìm kiếm tài liệu..." value={searchTerm} onChange={e=>setSearchTerm(e.target.value)}
                                className="w-full pl-10 pr-4 py-3 rounded-xl bg-white/80 border border-slate-200 shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"/>
                            <span className="absolute left-3 top-3.5 text-slate-400"><Search className="w-5 h-5"/></span>
                        </div>
                    </section>
                    {filtered.length > 0 ? (
                        <section className="mb-12 animate-fade-up delay-100">
                            <div className="max-w-2xl mx-auto space-y-4">
                                {filtered.map(rule => (
                                    <a key={rule.id} href={rule.url} target="_blank"
                                        className="group flex items-center justify-between px-6 py-5 bg-white rounded-2xl border border-slate-200 shadow-md hover:shadow-xl hover:-translate-y-0.5 hover:border-blue-300 transition-all duration-200"
                                        style={{textDecoration:'none'}}>
                                        <div className="flex items-center gap-4 flex-1">
                                            <div className="w-2.5 h-2.5 rounded-full bg-blue-500 group-hover:scale-125 transition-transform flex-shrink-0"></div>
                                            <span className="text-slate-700 font-semibold text-base group-hover:text-blue-600 transition-colors">{rule.title}</span>
                                        </div>
                                        <div className="flex items-center gap-2 text-slate-400 group-hover:text-blue-500 transition-colors flex-shrink-0 ml-4">
                                            <ExtLink className="w-4 h-4"/>
                                            <ChevRight className="w-4 h-4 group-hover:translate-x-1 transition-transform"/>
                                        </div>
                                    </a>
                                ))}
                            </div>
                        </section>
                    ) : (
                        <div className="text-center py-20 bg-white/40 rounded-3xl border border-dashed border-slate-300">
                            <Search className="w-12 h-12 text-slate-300 mx-auto mb-4"/>
                            <p className="text-slate-500 text-lg">Không tìm thấy tài liệu phù hợp.</p>
                        </div>
                    )}
                </main>
                <Footer/><ScrollToTop/>
            </div>
        );
    };

    /* ══════════════════════════════════════════
       KINH DOANH — DATA
    ══════════════════════════════════════════ */
    const kdSections = [
        { id:1, title:"I - TƯ VẤN BÁN HÀNG",
          icon:<Users className="w-5 h-5"/>, iconBg:"bg-blue-50", iconColor:"text-blue-600",
          desc:"Quy định bán hàng, xác thực Lead, quản lý KH trên CRM", count:7,
          focusItem:{ id:'1.1', title:"56QTKIOTVIET - QUY ĐỊNH BỘ PHẬN KINH DOANH",
            url:"https://drive.google.com/file/d/13zPshKY1FeCKIqTTQ9PaTrkfo415m4O4/view?usp=sharing",
            summary:{ regulations:[
              { title:"KHÁCH HÀNG VÀ QUẢN LÝ KHÁCH HÀNG TRÊN CRM", desc:["Tài khoản CRM","Phân chia khách hàng","Các nội dung bắt buộc phải xác thực khi tiếp cận khách hàng","Thu hồi Lead","Thu hồi Khách hàng tiềm năng","Khách hàng đăng ký dùng thử lại","Khách hàng giới thiệu KH","Tranh chấp KH","Chuyển giao khách hàng đến hạn tái ký","Tái ký KPI"] },
              { title:"QUY ĐỊNH VỀ VIỆC QUẢNG BÁ SẢN PHẨM", desc:"Tuân thủ các vấn đề liên quan đến hình ảnh, thương hiệu của công ty" },
              { title:"QUY ĐỊNH XỬ LÝ VI PHẠM", desc:["Vi phạm về hợp đồng","Vi phạm quy trình, quy định","Tự khai báo vi phạm"] }
            ]}},
          items:[
            {id:'1.2',title:"156QTKIOTVIET - QUY TRÌNH DUYỆT KHUYẾN MÃI TRÊN CRM",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tu-van/duyet-khuyen-mai"},
            {id:'1.3',title:"166QTKIOTVIET - QUY ĐỊNH TRỰC TỔNG ĐÀI BỘ PHẬN KINH DOANH",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tu-van/truc-tong-dai"},
            {id:'1.4',title:"172QTKIOTVIET - QUY TRÌNH GIA HẠN GIAN HÀNG DÙNG THỬ",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tu-van/gia-han-dung-thu"},
            {id:'1.5',title:"35QTKIOTVIET - QUY TRÌNH XÁC THỰC LEAD - BÁN HÀNG - CSKH",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tu-van/xac-thuc-lead"},
            {id:'1.6',title:"41QTKIOTVIET - QUY TRÌNH THU HỒI - GIA HẠN CONTACT",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tu-van/thu-hoi-contact"},
            {id:'1.7',title:"44QTKIOTVIET - QUY TRÌNH CHĂM SÓC KHÁCH HÀNG KHAI THÁC LẠI",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tu-van/cham-soc-khai-thac"},
          ]},
        { id:2, title:"II - THANH TOÁN - GHI NHẬN HỢP ĐỒNG",
          icon:<DollarSign className="w-5 h-5"/>, iconBg:"bg-green-50", iconColor:"text-green-600",
          desc:"Hướng dẫn thanh toán, ghi nhận hợp đồng, hoàn tiền", count:6,
          items:[
            {id:'2.1',title:"Hướng dẫn thanh toán cho khách hàng",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/thanh-toan/huong-dan"},
            {id:'2.2',title:"Các hình thức thanh toán được chấp nhận",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/thanh-toan/hinh-thuc"},
            {id:'2.3',title:"Quy trình ghi nhận hợp đồng trên hệ thống",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/thanh-toan/ghi-nhan"},
            {id:'2.4',title:"Kiểm tra và xác nhận thanh toán",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/thanh-toan/kiem-tra"},
            {id:'2.5',title:"Xử lý các trường hợp thanh toán đặc biệt",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/thanh-toan/dac-biet"},
            {id:'2.6',title:"Chính sách hoàn tiền",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/thanh-toan/hoan-tien"},
          ]},
        { id:3, title:"III - CHĂM SÓC SAU BÁN",
          icon:<CheckCircle className="w-5 h-5"/>, iconBg:"bg-purple-50", iconColor:"text-purple-600",
          desc:"Onboarding, chăm sóc định kỳ, loyalty & retention", count:5,
          items:[
            {id:'3.1',title:"Quy trình onboarding khách hàng mới",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/cham-soc/onboarding"},
            {id:'3.2',title:"Lịch chăm sóc định kỳ",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/cham-soc/lich-dinh-ky"},
            {id:'3.3',title:"Xử lý phản hồi và góp ý",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/cham-soc/phan-hoi"},
            {id:'3.4',title:"Chương trình loyalty & retention",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/cham-soc/loyalty"},
            {id:'3.5',title:"Up-sell và cross-sell",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/cham-soc/upsell"},
          ]},
        { id:4, title:"IV - TÁI KÝ",
          icon:<FileTextKD className="w-5 h-5"/>, iconBg:"bg-orange-50", iconColor:"text-orange-600",
          desc:"Quy trình tái ký, chính sách ưu đãi, theo dõi tỷ lệ", count:5,
          items:[
            {id:'4.1',title:"Quy trình tái ký hợp đồng",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tai-ky/quy-trinh"},
            {id:'4.2',title:"Thời điểm liên hệ tái ký",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tai-ky/thoi-diem"},
            {id:'4.3',title:"Chính sách ưu đãi cho khách hàng tái ký",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tai-ky/uu-dai"},
            {id:'4.4',title:"Xử lý khách hàng không tái ký",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tai-ky/xu-ly"},
            {id:'4.5',title:"Theo dõi tỷ lệ tái ký",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/tai-ky/theo-doi"},
          ]},
        { id:5, title:"V - QUY TRÌNH KHÁC",
          icon:<SettingsIco className="w-5 h-5"/>, iconBg:"bg-indigo-50", iconColor:"text-indigo-600",
          desc:"Xử lý lead, chuyển giao KH, báo cáo doanh số", count:5,
          items:[
            {id:'5.1',title:"Quy trình xử lý lead",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/quy-trinh-khac/lead"},
            {id:'5.2',title:"Quy trình chuyển giao khách hàng",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/quy-trinh-khac/chuyen-giao"},
            {id:'5.3',title:"Quy trình báo cáo doanh số",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/quy-trinh-khac/bao-cao"},
            {id:'5.4',title:"Quy trình đề xuất chính sách mới",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/quy-trinh-khac/de-xuat"},
            {id:'5.5',title:"Quy trình training nhân viên mới",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/quy-trinh-khac/training"},
          ]},
        { id:6, title:"VI - FINANCE - DỊCH VỤ TÀI CHÍNH",
          icon:<CreditCard className="w-5 h-5"/>, iconBg:"bg-teal-50", iconColor:"text-teal-600",
          desc:"Dịch vụ tài chính, vay vốn, phê duyệt hồ sơ", count:6,
          items:[
            {id:'6.1',title:"Giới thiệu dịch vụ tài chính KiotViet",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/finance/gioi-thieu"},
            {id:'6.2',title:"Quy trình vay vốn cho khách hàng",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/finance/vay-von"},
            {id:'6.3',title:"Điều kiện và hồ sơ vay vốn",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/finance/dieu-kien"},
            {id:'6.4',title:"Chính sách lãi suất và phí",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/finance/lai-suat"},
            {id:'6.5',title:"Theo dõi và thu hồi công nợ",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/finance/cong-no"},
            {id:'6.6',title:"Quy trình phê duyệt hồ sơ vay",url:"https://sites.google.com/kiotviet.com/coc/kinh-doanh/finance/phe-duyet"},
          ]},
    ];

    /* ── Modal chi tiết ── */
    const FocusModal = ({ item, onClose }) => {
        useEffect(() => {
            const k = e => { if (e.key==='Escape') onClose(); };
            window.addEventListener('keydown', k);
            return () => window.removeEventListener('keydown', k);
        }, []);
        return (
            <>
                <div className="spotlight-overlay" onClick={onClose}/>
                <button onClick={onClose} className="fixed top-4 right-4 z-[70] p-2.5 rounded-full bg-white text-slate-500 hover:text-slate-800 shadow-lg transition-all">
                    <XIco className="w-5 h-5"/>
                </button>
                <div className="fixed inset-0 z-[50] overflow-y-auto" onClick={onClose} style={{padding:'32px 24px'}}>
                    <div className="max-w-3xl mx-auto animate-scale-in" onClick={e=>e.stopPropagation()}>
                        <div className="text-center mb-4">
                            <div className="inline-flex items-center justify-center w-16 h-16 bg-blue-100 rounded-2xl mb-3 shadow-sm">
                                <BookOpenIco className="w-8 h-8 text-blue-600"/>
                            </div>
                            <h2 className="text-xl font-extrabold text-white leading-tight mb-1">{item.title}</h2>
                        </div>
                        <div className="bg-white rounded-2xl shadow-2xl overflow-hidden">
                            <div className="px-8 pt-6 pb-4 border-b border-slate-100 flex items-center gap-3">
                                <CheckCircle className="w-6 h-6 text-blue-500"/>
                                <span className="font-bold text-slate-800 text-lg">Nội dung chính</span>
                            </div>
                            <div className="px-8 py-2">
                                {item.summary.regulations.map((reg,i) => {
                                    const Ico = regIcons[i % regIcons.length];
                                    return (
                                        <div key={i} className="flex items-start gap-4 py-4 border-b border-slate-50 last:border-0"
                                            style={{opacity:0, animation:`slideDown 0.3s ease-out ${80+i*90}ms forwards`}}>
                                            <div className={`flex-shrink-0 w-10 h-10 rounded-xl reg-icon-${i%4} flex items-center justify-center mt-0.5`}>
                                                <Ico className="w-5 h-5"/>
                                            </div>
                                            <div className="flex-1">
                                                <p className="font-bold text-slate-800 text-base uppercase tracking-wide mb-2">{reg.title}</p>
                                                {Array.isArray(reg.desc) ? (
                                                    <ul className="space-y-1.5">
                                                        {reg.desc.map((d,j) => (
                                                            <li key={j} className="flex items-start gap-2 text-slate-500 text-sm">
                                                                <span className="flex-shrink-0 mt-1.5 w-1.5 h-1.5 rounded-full bg-blue-300"></span>
                                                                <span>{d}</span>
                                                            </li>
                                                        ))}
                                                    </ul>
                                                ) : (
                                                    <p className="text-slate-500 text-sm leading-relaxed">{reg.desc}</p>
                                                )}
                                            </div>
                                        </div>
                                    );
                                })}
                            </div>
                            <div className="px-8 pb-8 pt-4">
                                <a href={item.url} target="_blank"
                                    className="flex items-center justify-center gap-2.5 w-full py-4 bg-blue-600 hover:bg-blue-700 text-white font-bold text-base rounded-xl transition-all shadow-md">
                                    <FileTextKD className="w-5 h-5"/>Xem tài liệu đầy đủ<ExtLink className="w-4 h-4"/>
                                </a>
                            </div>
                        </div>
                    </div>
                </div>
            </>
        );
    };

    /* ── KD Section detail ── */
    const KDSectionPage = ({ section, onBack }) => {
        const [modal, setModal] = useState(false);
        useEffect(() => { window.scrollTo({top:0}); }, []);
        return (
            <div className="relative min-h-screen flex flex-col">
                {modal && section.focusItem && <FocusModal item={section.focusItem} onClose={()=>setModal(false)}/>}
                <BgShapes/>
                <header className="sticky top-0 z-30 bg-white/70 backdrop-blur-xl border-b border-slate-900/10">
                    <div className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
                        <div className="flex items-center justify-between h-16">
                            <div className="flex items-center gap-3">
                                <button onClick={onBack} className="flex items-center gap-2 px-3 py-1.5 rounded-lg text-slate-600 hover:text-blue-600 hover:bg-blue-50 transition-all font-medium text-sm">
                                    <ArrowLeft className="w-4 h-4"/><span className="hidden sm:inline">Quay lại</span>
                                </button>
                                <div className="h-4 w-px bg-slate-200"></div>
                                <img src="https://logo.kiotviet.vn/KiotViet-Logo-Horizontal.svg" alt="KiotViet" className="h-7"/>
                            </div>
                            <span className="text-slate-500 font-semibold text-xs sm:text-sm tracking-tight">{section.title}</span>
                        </div>
                    </div>
                </header>
                <main className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-10 md:py-14 flex-1">
                    <section className="mb-10 animate-fade-up">
                        <div className="flex items-center gap-3 mb-1">
                            <div className={`p-2.5 rounded-xl ${section.iconBg} ${section.iconColor} shadow-sm`}>{section.icon}</div>
                            <h1 className={`text-3xl md:text-4xl font-extrabold tracking-tight ${section.iconColor}`}>{section.title}</h1>
                        </div>
                        <p className="text-slate-500 mt-2 ml-14">{section.desc}</p>
                    </section>
                    <section className="animate-fade-up delay-100 pb-20 space-y-3">
                        {section.focusItem && (
                            <div className="focus-row" onClick={()=>setModal(true)}>
                                <div className="flex items-center gap-3 flex-1 min-w-0">
                                    <div className="w-2 h-2 rounded-full bg-blue-400 flex-shrink-0"></div>
                                    <span className="font-medium text-slate-700 text-sm">{section.focusItem.title}</span>
                                </div>
                                <div className="flex items-center gap-2 flex-shrink-0 ml-3">
                                    <span className="hidden sm:inline-flex items-center gap-1 text-xs font-semibold text-blue-500 bg-blue-50 border border-blue-200 px-3 py-1 rounded-full">+ Chi tiết</span>
                                    <ChevRight className="w-4 h-4 text-slate-400 chev-spin"/>
                                </div>
                            </div>
                        )}
                        {section.items.map(item => (
                            <a key={item.id} href={item.url} target="_blank" className="item-row">
                                <div className="flex items-center gap-3 flex-1 min-w-0">
                                    <div className="w-2 h-2 rounded-full bg-blue-400 flex-shrink-0"></div>
                                    <span className="font-medium text-slate-700 text-sm">{item.title}</span>
                                </div>
                                <div className="flex items-center gap-2 flex-shrink-0 ml-3">
                                    <span className="hidden sm:inline-flex items-center gap-1 text-xs font-semibold text-blue-500 bg-blue-50 border border-blue-200 px-3 py-1 rounded-full">+ Chi tiết</span>
                                    <ChevRight className="w-4 h-4 text-slate-400 chev-spin"/>
                                </div>
                            </a>
                        ))}
                    </section>
                </main>
                <Footer/><ScrollToTop/>
            </div>
        );
    };

    /* ══════════════════════════════════════════
       KINH DOANH INDEX PAGE
    ══════════════════════════════════════════ */
    const KinhDoanhPage = ({ onBack }) => {
        const [kdSection, setKdSection] = useState(null);

        if (kdSection !== null) {
            const sec = kdSections.find(s => s.id === kdSection);
            return <KDSectionPage section={sec} onBack={()=>{ setKdSection(null); window.scrollTo({top:0}); }}/>;
        }

        return (
            <div className="relative min-h-screen flex flex-col">
                <BgShapes/>
                <header className="sticky top-0 z-30 bg-white/70 backdrop-blur-xl border-b border-slate-900/10">
                    <div className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
                        <div className="flex items-center justify-between h-16">
                            <div className="flex items-center gap-3">
                                <button onClick={onBack} className="flex items-center gap-2 px-3 py-1.5 rounded-lg text-slate-600 hover:text-blue-600 hover:bg-blue-50 transition-all font-medium text-sm">
                                    <ArrowLeft className="w-4 h-4"/><span className="hidden sm:inline">Trang chủ</span>
                                </button>
                                <div className="h-4 w-px bg-slate-300 hidden sm:block"></div>
                                <img src="https://logo.kiotviet.vn/KiotViet-Logo-Horizontal.svg" alt="KiotViet" className="h-8"/>
                                <div className="h-4 w-px bg-slate-300 hidden sm:block"></div>
                                <span className="text-slate-600 font-semibold text-sm hidden sm:block tracking-tight">KINH DOANH</span>
                            </div>
                        </div>
                    </div>
                </header>
                <main className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-12 md:py-16 flex-1">
                    <nav className="flex items-center gap-2 text-sm text-slate-500 mb-10 animate-fade-up">
                        <button onClick={onBack} className="flex items-center gap-1.5 hover:text-blue-600 transition-colors font-medium">
                            <HomeIco className="w-4 h-4"/><span>Trang chủ</span>
                        </button>
                        <ChevRight className="w-4 h-4 text-slate-300"/>
                        <span className="text-slate-800 font-semibold">Quy trình - Kinh doanh</span>
                    </nav>
                    <section className="text-center mb-12 animate-fade-up">
                        <h1 className="text-4xl md:text-5xl font-extrabold text-slate-800 tracking-tight leading-tight">
                            QUY TRÌNH <span className="text-blue-600">KINH DOANH</span>
                        </h1>
                        <p className="mt-4 text-lg text-slate-600 max-w-2xl mx-auto font-medium">
                            Hướng dẫn chi tiết các quy trình bán hàng, chăm sóc khách hàng và dịch vụ tài chính
                        </p>
                    </section>
                    <section className="animate-fade-up delay-100 pb-20 space-y-4">
                        {kdSections.map(s => (
                            <div key={s.id} className="section-card" onClick={()=>{ setKdSection(s.id); window.scrollTo({top:0}); }}>
                                <div className="flex items-center gap-4 flex-1 min-w-0">
                                    <div className={`p-2.5 rounded-xl ${s.iconBg} ${s.iconColor} shadow-sm flex-shrink-0`}>{s.icon}</div>
                                    <div className="min-w-0">
                                        <h3 className="text-base md:text-lg font-bold text-slate-800 uppercase tracking-wide leading-tight">{s.title}</h3>
                                        <p className="text-xs text-slate-400 mt-0.5 font-normal normal-case truncate">{s.desc}</p>
                                    </div>
                                </div>
                                <div className="flex items-center gap-3 flex-shrink-0 ml-4">
                                    <span className="doc-count"><DocIco className="w-3.5 h-3.5"/>{s.count} tài liệu</span>
                                    <div className="kd-arrow-btn"><ChevRight className="w-4 h-4 chev-spin"/></div>
                                </div>
                            </div>
                        ))}
                    </section>
                </main>
                <Footer/><ScrollToTop/>
            </div>
        );
    };

    /* ══════════════════════════════════════════
       TRANG CHỦ
    ══════════════════════════════════════════ */
    const HomePage = ({ onNavigate }) => {
        const [searchTerm, setSearchTerm] = useState('');
        const filteredDocs = homeDocuments.filter(doc =>
            doc.title.toLowerCase().includes(searchTerm.toLowerCase()) ||
            doc.description.toLowerCase().includes(searchTerm.toLowerCase())
        );
        const DocCard = ({ doc }) => {
            const inner = (
                <>
                    <div className="flex items-center gap-4 mb-4">
                        <div className={`p-3 rounded-xl ${doc.bgClass} ${doc.colorClass} group-hover:scale-110 transition-transform duration-300`}>{doc.icon}</div>
                        <h3 className="text-xl font-bold text-slate-800 group-hover:text-blue-600 transition-colors">{doc.title}</h3>
                    </div>
                    <p className="text-slate-600 mb-6 flex-grow leading-relaxed">{doc.description}</p>
                    <div className={`mt-auto flex justify-between items-center w-full p-3 bg-slate-50/80 rounded-lg border border-slate-200 ${doc.hoverBorder} ${doc.hoverBg} transition-all group-hover:shadow-sm`}>
                        <span className="flex items-center gap-2 font-medium text-slate-700 text-sm">
                            {doc.internal
                                ? <><ArrowRight className="w-3.5 h-3.5 text-slate-400"/>Xem nội dung</>
                                : <><ExtLink className="w-3.5 h-3.5 text-slate-400"/>Truy cập</>}
                        </span>
                        <ArrowRight className="w-4 h-4 text-slate-400 group-hover:text-slate-600 group-hover:translate-x-1 transition-transform"/>
                    </div>
                </>
            );
            const cardClass = "group bg-white/60 backdrop-blur-lg rounded-2xl p-6 border border-slate-200 shadow-lg hover:shadow-2xl hover:-translate-y-1 transition-all duration-300 flex flex-col h-full cursor-pointer";
            if (doc.internal) {
                return (
                    <div className={cardClass} onClick={()=>{ onNavigate(doc.id); window.scrollTo({top:0}); }}>
                        {inner}
                    </div>
                );
            }
            return (
                <a href={doc.url} target="_blank" className={cardClass} style={{textDecoration:'none',color:'inherit'}}>
                    {inner}
                </a>
            );
        };

        return (
            <div className="relative min-h-screen flex flex-col">
                <BgShapes/>
                <header className="sticky top-0 z-50 bg-white/70 backdrop-blur-xl border-b border-slate-900/10">
                    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                        <div className="flex items-center justify-between h-16">
                            <div className="flex items-center gap-2 cursor-pointer" onClick={()=>window.scrollTo({top:0,behavior:'smooth'})}>
                                <img src="https://logo.kiotviet.vn/KiotViet-Logo-Horizontal.svg" alt="KiotViet" className="h-8"/>
                                <div className="h-4 w-px bg-slate-300 mx-2 hidden sm:block"></div>
                                <span className="text-slate-600 font-semibold text-sm hidden sm:block tracking-tight">Code of Conduct Hub</span>
                            </div>
                            <div className="hidden md:flex relative group">
                                <input type="text" placeholder="Tìm kiếm..." value={searchTerm} onChange={e=>setSearchTerm(e.target.value)}
                                    className="pl-9 pr-4 py-1.5 bg-slate-100/50 border-none rounded-full text-sm focus:ring-2 focus:ring-blue-500/50 transition-all w-48 group-hover:w-64 focus:w-64"/>
                                <span className="absolute left-3 top-2 text-slate-400"><Search className="w-4 h-4"/></span>
                            </div>
                        </div>
                    </div>
                </header>
                <main className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 md:py-16 flex-1">
                    <section className="text-center mb-16 animate-fade-up">
                        <h1 className="text-4xl md:text-5xl font-extrabold text-slate-800 tracking-tight leading-tight">
                            TÀI LIỆU <span className="text-blue-600">CODE OF CONDUCT</span>
                        </h1>
                        <p className="mt-4 text-lg text-slate-600 max-w-3xl mx-auto font-medium">
                            Cổng thông tin quy định, quy trình và chính sách dành cho bộ phận <br className="hidden md:block"/> Kinh doanh - DVKH - BO KiotViet
                        </p>
                        <div className="md:hidden mt-8 relative max-w-sm mx-auto">
                            <input type="text" placeholder="Tìm kiếm tài liệu..." value={searchTerm} onChange={e=>setSearchTerm(e.target.value)}
                                className="w-full pl-10 pr-4 py-3 rounded-xl bg-white/80 border border-slate-200 shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"/>
                            <span className="absolute left-3 top-3.5 text-slate-400"><Search className="w-5 h-5"/></span>
                        </div>
                    </section>
                    <section className="animate-fade-up delay-100 pb-20">
                        {filteredDocs.length > 0 ? (
                            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 lg:gap-8">
                                {filteredDocs.map(doc => <DocCard key={doc.id} doc={doc}/>)}
                            </div>
                        ) : (
                            <div className="text-center py-20 bg-white/40 backdrop-blur-md rounded-3xl border border-dashed border-slate-300">
                                <Search className="w-12 h-12 text-slate-300 mx-auto mb-4"/>
                                <p className="text-slate-500 text-lg">Không tìm thấy tài liệu phù hợp.</p>
                            </div>
                        )}
                    </section>
                </main>
                <Footer/><ScrollToTop/>
            </div>
        );
    };

    /* ══════════════════════════════════════════
       ROOT APP
    ══════════════════════════════════════════ */
    const App = () => {
        const [page, setPage] = useState('home');
        const goHome = () => { setPage('home'); window.scrollTo({top:0}); };

        if (page === 'quy-dinh-chung') return <QuyDinhChungPage onBack={goHome}/>;
        if (page === 'kinh-doanh')     return <KinhDoanhPage onBack={goHome}/>;
        return <HomePage onNavigate={id => {
            if (id === 1) setPage('quy-dinh-chung');
            if (id === 2) setPage('kinh-doanh');
        }}/>;
    };

    ReactDOM.createRoot(document.getElementById('root')).render(<App/>);
</script>
</body>
</html>
