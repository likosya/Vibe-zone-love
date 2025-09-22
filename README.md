# Vibe-zone-love
import React, { useState } from "react";
import { motion } from "framer-motion";
import { Heart, Camera, Video, Flower2, Sparkles, Check, Phone, Send, Instagram, MessageSquare, Clock, MapPin, Languages, ShieldCheck, Calendar } from "lucide-react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";

/**
 * DateSpark — одностраничный сайт для продажи услуги «Свидания под ключ»
 * Аудитория: русскоязычные в Корее
 * Автор: Artem + ChatGPT
 * Технологии: React + Tailwind + shadcn/ui + framer-motion
 *
 * Что внутри:
 * - Нейромаркетинговая цветовая палитра (романтическая, заметная, продающая)
 * - УТП блоки, оффер, социальные доказательства, пакеты с ценами, FAQ, форма заявки
 * - Готово к быстрой локализации RU/KR
 */

// Цвета: "магнит" внимания — тёплый градиент розовый→персиковый с акцентом шампань/золото
const GRADIENT_BG = "bg-[radial-gradient(ellipse_at_top_right,_#ffdef0_0%,_#ffd1dc_25%,_#ffc6c6_45%,_#ffb5a7_65%,_#ffa6a6_80%,_#ffd6a5_100%)]";
const ACCENT = "#FF5C8A"; // акцентные элементы и CTA
const ACCENT_DARK = "#E34C79";
const GOLD = "#D9A441"; // штрихи роскоши

const navItems = [
  { id: "services", label: "Услуги" },
  { id: "packages", label: "Пакеты" },
  { id: "gallery", label: "Галерея" },
  { id: "faq", label: "FAQ" },
  { id: "contact", label: "Заявка" },
];

const services = [
  {
    icon: <Camera className="w-6 h-6" />, title: "Фотограф",
    text: "Эмоциональные кадры для альбома и соцсетей. Работаем в любом стиле: lifestyle, film, luxury.",
  },
  {
    icon: <Video className="w-6 h-6" />, title: "Видеограф",
    text: "Теплый сторис-ролик и клип на 60–120 сек. Профессиональный звук и цветокор.",
  },
  {
    icon: <Flower2 className="w-6 h-6" />, title: "Флорист",
    text: "Индивидуальные букеты/декор под характер пары. Свежая флора из лучших студий KR.",
  },
  {
    icon: <Sparkles className="w-6 h-6" />, title: "Организация",
    text: "Сценарий, площадка, реквизит, музыка, погодный план B. Вы — только наслаждаетесь.",
  },
];

const packages = [
  {
    name: "Light",
    price: "₩390,000",
    tagline: "Тёплая мини-встреча",
    features: [
      "Консультация и сценарий 30 мин",
      "Декор точки встречи (лайт)",
      "Букет стандарт",
      "Фотосъёмка 1 час (30+ фото)",
      "Видеосторис до 30 сек",
      "Поддержка в Telegram/Kakao",
    ],
    best: false,
  },
  {
    name: "Classic",
    price: "₩690,000",
    tagline: "Самый популярный",
    features: [
      "Полный сценарий и плейлист",
      "Декор зоны (свечи/гирлянды)",
      "Букет premium",
      "Фотосъёмка 2 часа (70+ фото)",
      "Видеоклип 60–90 сек",
      "Бронь локации (согласуем)",
    ],
    best: true,
  },
  {
    name: "Luxury",
    price: "₩1,290,000",
    tagline: "Вау-эффект",
    features: [
      "Индивидуальная концепция",
      "Авторский декор + неон",
      "Букет signature",
      "Фото 3 часа (120+ фото)",
      "Фильм 120 сек + бэкстейдж",
      "Трансфер + ассистент",
    ],
    best: false,
  },
];

const faqs = [
  {
    q: "Вы работаете только в Сеуле?",
    a: "База — Сеул/Чхонан/Асан. Ездим по всей Корее: Инчхон, Пусан, Тэгу, Чеджу — согласуем логистику заранее.",
  },
  {
    q: "Как бронировать дату?",
    a: "Оставьте заявку и внесите предоплату 20%. Мы закрепим слоты команды и начнём подготовку.",
  },
  {
    q: "Можно ли адаптировать под бюджет?",
    a: "Да. Подберём формат под ваш запрос: от минималистичного пикника до приватного ужина с живой музыкой.",
  },
  {
    q: "Нужна корейская версия сайта",
    a: "Мы общаемся на русском и корейском. Переключатель RU/KR в шапке, сопровождение — на удобном языке.",
  },
];

export default function DateSparkLanding() {
  const [lang, setLang] = useState<'RU' | 'KR'>("RU");
  const t = (ru: string, kr: string) => (lang === "RU" ? ru : kr);

  return (
    <div className={`min-h-screen text-zinc-900 ${GRADIENT_BG}`}>
      {/* Header */}
      <header className="sticky top-0 z-50 backdrop-blur supports-[backdrop-filter]:bg-white/60 bg-white/50 border-b border-white/30">
        <div className="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between">
          <div className="flex items-center gap-2">
            <Heart style={{ color: ACCENT }} className="w-6 h-6" />
            <span className="font-semibold tracking-tight">DateSpark Korea</span>
          </div>
          <nav className="hidden md:flex items-center gap-6 text-sm">
            {navItems.map((n) => (
              <a key={n.id} href={`#${n.id}`} className="hover:opacity-80 transition">{n.label}</a>
            ))}
          </nav>
          <div className="flex items-center gap-2">
            <Button onClick={() => setLang((p) => (p === 'RU' ? 'KR' : 'RU'))} variant="outline" className="h-9">
              <Languages className="w-4 h-4 mr-2" /> {lang === 'RU' ? 'KR' : 'RU'}
            </Button>
            <a href="#contact"><Button className="h-9" style={{ backgroundColor: ACCENT, color: "white" }}>Забронировать</Button></a>
          </div>
        </div>
      </header>

      {/* Hero */}
      <section className="relative overflow-hidden">
        <div className="max-w-6xl mx-auto px-4 py-20 grid md:grid-cols-2 gap-10 items-center">
          <div>
            <motion.h1
              initial={{ opacity: 0, y: 20 }}
              whileInView={{ opacity: 1, y: 0 }}
              transition={{ duration: 0.6 }}
              className="text-4xl md:text-6xl font-extrabold leading-tight tracking-tight"
            >
              {t(
                "Зажигаем пары и делаем отношения ещё краше",
                "우리는 커플의 마음에 불을 지피고 관계를 더 아름답게 만듭니다"
              )}
            </motion.h1>
            <p className="mt-5 text-base md:text-lg text-zinc-700">
              {t(
                "Свидание под ключ в Корее: сценарий, декор, фото/видео и полная забота. Вы — только наслаждаетесь.",
                "한국에서 올인원 데이트 연출: 시나리오·데코·사진/영상까지, 당신은 사랑만 즐기세요."
              )}
            </p>
            <div className="mt-7 flex flex-wrap gap-3">
              <a href="#packages"><Button size="lg" style={{ backgroundColor: ACCENT, color: "white" }}>
                <Sparkles className="w-5 h-5 mr-2" /> {t("Выбрать пакет", "패키지 보기")}
              </Button></a>
              <a href="#contact"><Button size="lg" variant="outline">
                <Phone className="w-5 h-5 mr-2" /> {t("Связаться", "문의하기")}
              </Button></a>
            </div>
            <div className="mt-6 flex items-center gap-4 text-sm text-zinc-700">
              <div className="flex items-center gap-2"><ShieldCheck className="w-4 h-4" /> {t("Договор и чек", "계약·영수증 제공")}</div>
              <div className="flex items-center gap-2"><Clock className="w-4 h-4" /> {t("Гибкое время", "유연한 일정")}</div>
              <div className="flex items-center gap-2"><MapPin className="w-4 h-4" /> {t("Вся Корея", "대한민국 전역")}</div>
            </div>
          </div>
          <div className="relative">
            <div className="aspect-[4/5] rounded-3xl shadow-2xl overflow-hidden ring-4 ring-white/50">
              {/* Заглушка под будущую карусель фото/видео */}
              <div className="w-full h-full bg-white/40 backdrop-blur flex items-center justify-center">
                <div className="text-center p-8">
                  <div className="flex items-center justify-center gap-2 text-xl font-semibold">
                    <Camera /> <Video /> <Flower2 />
                  </div>
                  <p className="mt-3 text-sm text-zinc-700">Здесь будет слайдер ваших работ (фото/видео)</p>
                </div>
              </div>
            </div>
            <div className="absolute -bottom-6 -left-6 rotate-[-6deg]">
              <span className="inline-block px-4 py-2 rounded-xl text-white text-sm font-semibold shadow-lg" style={{ background: GOLD }}>TOP choice</span>
            </div>
          </div>
        </div>
      </section>

      {/* Services */}
      <section id="services" className="py-16">
        <div className="max-w-6xl mx-auto px-4">
          <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Что входит</h2>
          <div className="mt-8 grid md:grid-cols-4 gap-6">
            {services.map((s, i) => (
              <Card key={i} className="bg-white/70 border-white/40 shadow-sm">
                <CardContent className="p-6">
                  <div className="w-10 h-10 rounded-full flex items-center justify-center mb-4" style={{ backgroundColor: ACCENT + "20", color: ACCENT }}>
                    {s.icon}
                  </div>
                  <div className="font-semibold">{s.title}</div>
                  <p className="mt-2 text-sm text-zinc-700">{s.text}</p>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* Packages */}
      <section id="packages" className="py-16">
        <div className="max-w-6xl mx-auto px-4">
          <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Пакеты</h2>
          <p className="mt-2 text-zinc-700">Цены ориентировочные — финальная смета зависит от локации и даты.</p>
          <div className="mt-8 grid md:grid-cols-3 gap-6">
            {packages.map((p, i) => (
              <Card key={i} className={`border-2 ${p.best ? "border-["+ACCENT+"] shadow-xl scale-[1.02]" : "border-white/50"} bg-white/75`}>
                <CardContent className="p-6">
                  <div className="flex items-center justify-between">
                    <div>
                      <div className="text-xl font-extrabold tracking-tight">{p.name}</div>
                      <div className="text-sm text-zinc-600">{p.tagline}</div>
                    </div>
                    {p.best && (
                      <span className="px-3 py-1 text-xs rounded-full text-white" style={{ backgroundColor: ACCENT_DARK }}>Хит</span>
                    )}
                  </div>
                  <div className="mt-4 text-3xl font-bold" style={{ color: ACCENT }}>{p.price}</div>
                  <ul className="mt-4 space-y-2 text-sm">
                    {p.features.map((f, idx) => (
                      <li key={idx} className="flex gap-2">
                        <Check className="w-4 h-4 mt-0.5" style={{ color: GOLD }} />
                        <span>{f}</span>
                      </li>
                    ))}
                  </ul>
                  <a href="#contact"><Button className="w-full mt-6" style={{ backgroundColor: ACCENT, color: "white" }}>Выбрать {p.name}</Button></a>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* Gallery placeholder */}
      <section id="gallery" className="py-16">
        <div className="max-w-6xl mx-auto px-4">
          <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Галерея</h2>
          <p className="mt-2 text-zinc-700">Подключим ваши лучшие съёмки — добавим до 12 карточек и видео-обложку.</p>
          <div className="mt-8 grid grid-cols-2 md:grid-cols-4 gap-4">
            {Array.from({ length: 8 }).map((_, i) => (
              <div key={i} className="aspect-square rounded-2xl bg-white/60 ring-1 ring-white/50 shadow-sm flex items-center justify-center text-zinc-500">
                <span>Фото {i + 1}</span>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Testimonials (соц.доказательства) */}
      <section className="py-16">
        <div className="max-w-6xl mx-auto px-4">
          <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Отзывы</h2>
          <div className="mt-8 grid md:grid-cols-3 gap-6">
            {[1, 2, 3].map((n) => (
              <Card key={n} className="bg-white/75">
                <CardContent className="p-6">
                  <div className="flex items-center gap-2 font-semibold"><Heart className="w-4 h-4" style={{ color: ACCENT }} /> Пара #{n}</div>
                  <p className="mt-2 text-sm text-zinc-700">«Это было волшебно! Организация 10/10, фото и видео — огонь, мы пересматриваем каждый день.»</p>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* FAQ */}
      <section id="faq" className="py-16">
        <div className="max-w-6xl mx-auto px-4">
          <h2 className="text-2xl md:text-4xl font-bold tracking-tight">FAQ</h2>
          <div className="mt-6 grid md:grid-cols-2 gap-6">
            {faqs.map((f, i) => (
              <Card key={i} className="bg-white/75">
                <CardContent className="p-6">
                  <div className="font-semibold flex items-center gap-2"><MessageSquare className="w-4 h-4" /> {f.q}</div>
                  <p className="mt-2 text-sm text-zinc-700">{f.a}</p>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* Contact */}
      <section id="contact" className="py-16">
        <div className="max-w-6xl mx-auto px-4">
          <h2 className="text-2xl md:text-4xl font-bold tracking-tight">Заявка</h2>
          <div className="mt-6 grid md:grid-cols-2 gap-6">
            <Card className="bg-white/80">
              <CardContent className="p-6">
                <form className="space-y-4" method="POST" action="#">
                  <div className="grid md:grid-cols-2 gap-4">
                    <div>
                      <label className="text-sm">Имя</label>
                      <Input name="name" placeholder="Артём" required />
                    </div>
                    <div>
                      <label className="text-sm">Мессенджер</label>
                      <Input name="messenger" placeholder="Telegram/Kakao/WhatsApp" />
                    </div>
                  </div>
                  <div className="grid md:grid-cols-2 gap-4">
                    <div>
                      <label className="text-sm">Дата</label>
                      <Input name="date" type="date" />
                    </div>
                    <div>
                      <label className="text-sm">Город</label>
                      <Input name="city" placeholder="Сеул / Пусан / Чеджу…" />
                    </div>
                  </div>
                  <div>
                    <label className="text-sm">Комментарий</label>
                    <Textarea name="comment" placeholder="Хочу предложение руки и сердца под звёздами…" rows={4} />
                  </div>
                  <Button type="submit" className="w-full" style={{ backgroundColor: ACCENT, color: "white" }}>
                    <Send className="w-4 h-4 mr-2" /> Отправить заявку
                  </Button>
                  <p className="text-xs text-zinc-600">
                    Нажимая кнопку, вы соглашаетесь с обработкой персональных данных и политикой конфиденциальности.
                  </p>
                </form>
              </CardContent>
            </Card>
            <div className="space-y-4">
              <Card className="bg-white/80">
                <CardContent className="p-6">
                  <div className="font-semibold">Быстрая связь</div>
                  <div className="mt-3 grid grid-cols-2 gap-3">
                    <a href="https://t.me/" target="_blank" rel="noreferrer">
                      <Button variant="outline" className="w-full"><Send className="w-4 h-4 mr-2" /> Telegram</Button>
                    </a>
                    <a href="https://open.kakao.com/" target="_blank" rel="noreferrer">
                      <Button variant="outline" className="w-full"><MessageSquare className="w-4 h-4 mr-2" /> KakaoTalk</Button>
                    </a>
                    <a href="tel:+821042041403"><Button variant="outline" className="w-full"><Phone className="w-4 h-4 mr-2" /> Позвонить</Button></a>
                    <a href="https://instagram.com/" target="_blank" rel="noreferrer">
                      <Button variant="outline" className="w-full"><Instagram className="w-4 h-4 mr-2" /> Instagram</Button>
                    </a>
                  </div>
                </CardContent>
              </Card>
              <Card className="bg-white/80">
                <CardContent className="p-6">
                  <div className="font-semibold flex items-center gap-2"><Calendar className="w-4 h-4" /> Как мы работаем</div>
                  <ol className="mt-3 list-decimal list-inside text-sm text-zinc-700 space-y-1">
                    <li>Заявка → уточняем пожелания и бюджет</li>
                    <li>Закрепляем дату по предоплате 20%</li>
                    <li>Подбор локации и декора, составление сценария</li>
                    <li>Съёмочный план и тайминг под погоду</li>
                    <li>Съёмка, вау-моменты, передача материалов</li>
                  </ol>
                </CardContent>
              </Card>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="py-12 border-t border-white/40 bg-white/50">
        <div className="max-w-6xl mx-auto px-4 grid md:grid-cols-3 gap-6 items-center">
          <div className="text-sm">
            © {new Date().getFullYear()} DateSpark Korea. Все права защищены.
          </div>
          <div className="text-center text-sm">
            Политика конфиденциальности · Договор-оферта
          </div>
          <div className="md:text-right text-sm">
            Сделано с любовью в Корее 🇰🇷
          </div>
        </div>
      </footer>
    </div>
  );
}
