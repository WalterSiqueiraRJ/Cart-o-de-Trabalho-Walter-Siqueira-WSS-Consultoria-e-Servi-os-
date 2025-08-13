# Cart-o-de-Trabalho-Walter-Siqueira-WSS-Consultoria-e-Servi-os-
Consultoria e Serviços em Técnologia e Eletrônica
import { useMemo } from "react";
import { motion } from "framer-motion";
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Linkedin, Phone, MessageCircle, Cpu, ShieldCheck, Wrench, Home, Sparkles } from "lucide-react";

export default function DigitalBusinessCard() {
  const name = "Walter Siqueira";
  const company = "WSS Consultoria e Serviços";
  const role = "Consultor de TI & Instrutor";
  const whatsapp = "+55 21 98206-9957";
  const whatsappLink = "https://wa.me/5521982069957";
  const linkedin = "https://www.linkedin.com/in/walter-siqueira-39110521";

  const vcardData = useMemo(() => {
    const lines = [
      "BEGIN:VCARD",
      "VERSION:3.0",
      `N:Siqueira;Walter;;;`,
      `FN:${name}`,
      `ORG:${company}`,
      `TITLE:${role}`,
      `TEL;TYPE=CELL,VOICE:${whatsapp}`,
      `URL:${linkedin}`,
      "END:VCARD",
    ];
    return lines.join("\r\n");
  }, []);

  const downloadVCard = () => {
    const blob = new Blob([vcardData], { type: "text/vcard;charset=utf-8" });
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = "WalterSiqueira.vcf";
    document.body.appendChild(a);
    a.click();
    a.remove();
    URL.revokeObjectURL(url);
  };

  return (
    <div className="min-h-screen w-full bg-gradient-to-b from-slate-900 via-slate-950 to-black text-white flex items-center justify-center p-6">
      <Card className="w-full max-w-3xl rounded-2xl border-0 shadow-xl bg-white/5 backdrop-blur-xl">
        <CardHeader className="pb-0">
          <div className="flex items-center gap-4">
            {/* Avatar with initials */}
            <motion.div
              initial={{ opacity: 0, y: 10 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ duration: 0.4 }}
              className="size-16 rounded-2xl bg-gradient-to-br from-blue-500/80 to-cyan-400/80 grid place-content-center font-bold text-2xl shadow-lg"
            >
              WS
            </motion.div>
            <div className="flex-1">
              <CardTitle className="text-2xl sm:text-3xl font-semibold flex items-center gap-2">
                {company}
                <Sparkles className="size-5 opacity-70" />
              </CardTitle>
              <p className="text-sm sm:text-base text-slate-300 mt-1">
                {name} • {role}
              </p>
            </div>
          </div>
        </CardHeader>
        <CardContent className="pt-6">
          {/* Services grid */}
          <div className="grid sm:grid-cols-2 gap-4">
            <Service
              icon={<Cpu className="size-5" />}
              title="Aulas On-line"
              items={["Inteligência Artificial (IA)", "LGPD – Lei Geral de Proteção de Dados"]}
            />
            <Service
              icon={<Wrench className="size-5" />}
              title="Serviços Técnicos"
              items={["Conserto de TV e eletrodomésticos", "Instalação e configuração de equipamentos"]}
            />
            <Service
              icon={<Home className="size-5" />}
              title="Automação Residencial"
              items={["Casa Inteligente integrada com Alexa", "Câmeras, sensores, iluminação smart"]}
            />
            <Service
              icon={<ShieldCheck className="size-5" />}
              title="Qualidade & Confiabilidade"
              items={["Atendimento personalizado", "Soluções sob medida"]}
            />
          </div>

          {/* Action buttons */}
          <div className="mt-6 grid grid-cols-1 sm:grid-cols-3 gap-3">
            <Button
              onClick={() => window.open(whatsappLink, "_blank")}
              className="rounded-2xl h-12 text-base"
            >
              <MessageCircle className="mr-2 size-5" /> WhatsApp
            </Button>
            <Button
              variant="secondary"
              onClick={() => window.open(linkedin, "_blank")}
              className="rounded-2xl h-12 text-base"
            >
              <Linkedin className="mr-2 size-5" /> LinkedIn
            </Button>
            <Button
              variant="outline"
              onClick={downloadVCard}
              className="rounded-2xl h-12 text-base border-white/30"
            >
              <Phone className="mr-2 size-5" /> Salvar Contato (VCF)
            </Button>
          </div>

          {/* Contact line */}
          <div className="mt-6 text-center text-sm text-slate-300">
            <p>
              Fale agora: <span className="font-medium">{whatsapp}</span>
            </p>
          </div>
        </CardContent>
      </Card>
    </div>
  );
}

function Service({ icon, title, items }: { icon: React.ReactNode; title: string; items: string[] }) {
  return (
    <motion.div
      initial={{ opacity: 0, y: 8 }}
      animate={{ opacity: 1, y: 0 }}
      transition={{ duration: 0.35 }}
      className="rounded-2xl p-4 bg-white/5 border border-white/10 shadow-sm"
    >
      <div className="flex items-center gap-2 mb-2">
        <div className="size-8 rounded-xl bg-white/10 grid place-content-center">{icon}</div>
        <h3 className="font-semibold">{title}</h3>
      </div>
      <ul className="text-sm text-slate-300 space-y-1 list-disc ml-6">
        {items.map((it, i) => (
          <li key={i}>{it}</li>
        ))}
      </ul>
    </motion.div>
  );
}
