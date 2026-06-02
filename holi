import React, { useState } from 'react';
import { Calendar, Trash2, Info } from 'lucide-react';

const holidays2026 = {
  "2026-01-01": "Año Nuevo",
  "2026-01-06": "Reyes Magos",
  "2026-04-03": "Viernes Santo",
  "2026-04-06": "Lunes de Pascua",
  "2026-05-01": "Día del Trabajador",
  "2026-05-25": "Segunda Pascua (Pascua Granada)", // Local BCN
  "2026-06-24": "Sant Joan",
  "2026-08-15": "La Asunción",
  "2026-09-11": "La Diada",
  "2026-09-24": "La Mercè", // Local BCN
  "2026-10-12": "Fiesta Nacional de España",
  "2026-11-01": "Todos los Santos",
  "2026-12-06": "Día de la Constitución",
  "2026-12-08": "Inmaculada Concepción",
  "2026-12-25": "Navidad",
  "2026-12-26": "Sant Esteve"
};

const months = [
  "Enero", "Febrero", "Marzo", "Abril", "Mayo", "Junio", 
  "Julio", "Agosto", "Septiembre", "Octubre", "Noviembre", "Diciembre"
];

const daysOfWeek = ['L', 'M', 'X', 'J', 'V', 'S', 'D'];

export default function App() {
  const [selectedDays, setSelectedDays] = useState(new Set());

  // Helper functions for calendar logic
  const getDaysInMonth = (year, month) => new Date(year, month + 1, 0).getDate();
  const getFirstDayOfWeek = (year, month) => {
    let day = new Date(year, month, 1).getDay();
    return day === 0 ? 6 : day - 1; // Adjust so Monday is 0 and Sunday is 6
  };

  const toggleDay = (dateStr) => {
    const newSet = new Set(selectedDays);
    if (newSet.has(dateStr)) {
      newSet.delete(dateStr);
    } else {
      newSet.add(dateStr);
    }
    setSelectedDays(newSet);
  };

  const clearDays = () => setSelectedDays(new Set());

  return (
    <div className="min-h-screen bg-slate-50 text-slate-800 font-sans pb-12 selection:bg-blue-100">
      
      {/* Sticky Header */}
      <header className="sticky top-0 bg-white/80 backdrop-blur-md border-b border-slate-200 z-50">
        <div className="max-w-6xl mx-auto px-4 py-4 flex flex-col sm:flex-row justify-between items-center gap-4">
          <div className="flex items-center gap-3">
            <div className="p-2.5 bg-blue-600 rounded-xl text-white shadow-sm shadow-blue-200">
              <Calendar size={24} />
            </div>
            <div>
              <h1 className="text-xl sm:text-2xl font-bold text-slate-900 leading-tight">Planificador 2026</h1>
              <p className="text-sm font-medium text-slate-500">Calendario laboral - Barcelona</p>
            </div>
          </div>
          
          <div className="flex items-center gap-4 w-full sm:w-auto justify-between sm:justify-end">
            {selectedDays.size > 0 && (
              <button 
                onClick={clearDays}
                className="flex items-center gap-1.5 text-sm font-semibold text-slate-500 hover:text-red-600 transition-colors px-2 py-1"
              >
                <Trash2 size={16} />
                <span>Limpiar</span>
              </button>
            )}
            <div className="bg-slate-900 text-white px-5 py-2.5 rounded-full flex items-center gap-3 shadow-lg hover:shadow-xl transition-shadow cursor-default">
              <span className="text-2xl font-black tabular-nums">{selectedDays.size}</span>
              <span className="text-sm font-medium leading-tight text-slate-300 border-l border-slate-700 pl-3">días<br/>tomados</span>
            </div>
          </div>
        </div>
      </header>

      <main className="max-w-6xl mx-auto px-4 mt-8">
        
        {/* Interactive Legend */}
        <div className="bg-white rounded-2xl p-4 sm:p-5 shadow-sm border border-slate-200/60 flex flex-wrap justify-center gap-6 sm:gap-8 mb-8 text-sm font-medium text-slate-600">
          <div className="flex items-center gap-2.5">
            <div className="w-5 h-5 rounded-md border border-slate-200 bg-white"></div> 
            Días laborables
          </div>
          <div className="flex items-center gap-2.5">
            <div className="w-5 h-5 rounded-md bg-slate-100 border border-slate-200/50"></div> 
            Fin de semana
          </div>
          <div className="flex items-center gap-2.5">
            <div className="w-5 h-5 rounded-md bg-red-50 border border-red-200 flex items-center justify-center">
              <div className="w-1.5 h-1.5 rounded-full bg-red-500"></div>
            </div> 
            Festivo BCN
          </div>
          <div className="flex items-center gap-2.5">
            <div className="w-5 h-5 rounded-md bg-blue-600 shadow-sm shadow-blue-200 ring-2 ring-blue-600 ring-offset-1"></div> 
            Día seleccionado
          </div>
        </div>

        {/* 12-Month Calendar Grid */}
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
          {months.map((monthName, monthIndex) => {
            const year = 2026;
            const daysInMonth = getDaysInMonth(year, monthIndex);
            const firstDay = getFirstDayOfWeek(year, monthIndex);
            
            const blanks = Array.from({ length: firstDay });
            const monthDays = Array.from({ length: daysInMonth }, (_, i) => i + 1);

            return (
              <div key={monthName} className="bg-white rounded-3xl p-5 shadow-sm border border-slate-200/60">
                <h2 className="text-lg font-bold text-slate-800 mb-4 ml-1 capitalize tracking-wide">{monthName}</h2>
                
                {/* Days of Week Header */}
                <div className="grid grid-cols-7 gap-1 text-center mb-3">
                  {daysOfWeek.map(d => (
                    <div key={d} className="text-[11px] font-bold text-slate-400 uppercase tracking-wider">{d}</div>
                  ))}
                </div>
                
                {/* Dates Grid */}
                <div className="grid grid-cols-7 gap-1.5">
                  {blanks.map((_, i) => <div key={`blank-${i}`} className="aspect-square" />)}
                  
                  {monthDays.map(d => {
                    const dateStr = `${year}-${String(monthIndex + 1).padStart(2, '0')}-${String(d).padStart(2, '0')}`;
                    const isHoliday = !!holidays2026[dateStr];
                    const holidayName = holidays2026[dateStr];
                    const dayOfWeek = new Date(year, monthIndex, d).getDay();
                    const isWeekend = dayOfWeek === 0 || dayOfWeek === 6;
                    const isSelected = selectedDays.has(dateStr);

                    // Base button styling
                    let btnClass = "relative aspect-square w-full flex items-center justify-center rounded-xl text-sm font-semibold transition-all active:scale-90 border outline-none focus-visible:ring-2 focus-visible:ring-slate-400 ";

                    // Layered visual priority: Selected > Holiday > Weekend > Workday
                    if (isSelected) {
                      btnClass += "bg-blue-600 text-white border-blue-600 shadow-md ring-2 ring-blue-600 ring-offset-1 z-10 hover:bg-blue-700";
                    } else if (isHoliday) {
                      btnClass += "bg-red-50 text-red-700 border-red-200 hover:bg-red-100 hover:border-red-300";
                    } else if (isWeekend) {
                      btnClass += "bg-slate-100 text-slate-500 border-transparent hover:bg-slate-200 hover:text-slate-700";
                    } else {
                      btnClass += "bg-white text-slate-700 border-slate-200 hover:border-blue-300 hover:bg-blue-50";
                    }

                    return (
                      <button
                        key={d}
                        onClick={() => toggleDay(dateStr)}
                        title={isHoliday ? holidayName : isWeekend ? 'Fin de semana' : 'Laborable'}
                        className={btnClass}
                      >
                        {d}
                        
                        {/* Little dot indicator for unselected holidays so they are very clear */}
                        {!isSelected && isHoliday && (
                           <div className="absolute bottom-1 w-1 h-1 rounded-full bg-red-500"></div>
                        )}
                      </button>
                    );
                  })}
                </div>
              </div>
            );
          })}
        </div>

        {/* Tip Section */}
        <div className="mt-8 bg-blue-50 text-blue-800 rounded-2xl p-4 flex gap-3 items-start border border-blue-100">
           <Info className="shrink-0 mt-0.5" size={20} />
           <p className="text-sm font-medium leading-relaxed">
             <strong>Tip:</strong> Pasa el ratón (hover) sobre los días marcados en rojo para ver el nombre específico del festivo (ej: La Mercè, Segunda Pascua, etc). Haz clic en cualquier día para sumarlo a tus días totales de vacaciones tomados.
           </p>
        </div>

      </main>
    </div>
  );
}
