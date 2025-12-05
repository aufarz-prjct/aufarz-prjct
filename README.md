import React, { useState, useEffect } from 'react';
import { Flame, Swords, Skull, Crown, Zap, Shield, Code, GitBranch, Star } from 'lucide-react';

export default function FantasyProfile() {
  const [dragonPos, setDragonPos] = useState({ x: 0, y: 0 });
  const [particles, setParticles] = useState([]);
  const [hoveredCard, setHoveredCard] = useState(null);

  useEffect(() => {
    const moveInterval = setInterval(() => {
      setDragonPos({
        x: Math.sin(Date.now() / 1000) * 50,
        y: Math.sin(Date.now() / 800) * 30
      });
    }, 50);

    const particleInterval = setInterval(() => {
      setParticles(prev => [
        ...prev.slice(-20),
        {
          id: Date.now(),
          x: Math.random() * 100,
          y: Math.random() * 100,
          size: Math.random() * 4 + 2,
          duration: Math.random() * 3 + 2
        }
      ]);
    }, 200);

    return () => {
      clearInterval(moveInterval);
      clearInterval(particleInterval);
    };
  }, []);

  const stats = [
    { icon: Flame, label: 'Lines of Code', value: '100K+', color: 'from-red-600 to-orange-500' },
    { icon: Skull, label: 'Bugs Slain', value: '999+', color: 'from-purple-600 to-pink-500' },
    { icon: Swords, label: 'Projects Forged', value: '50+', color: 'from-blue-600 to-cyan-500' },
    { icon: Crown, label: 'Commits Made', value: '5K+', color: 'from-yellow-600 to-amber-500' }
  ];

  const skills = [
    { name: 'JavaScript', level: 95, color: 'bg-yellow-500' },
    { name: 'Python', level: 90, color: 'bg-blue-500' },
    { name: 'React', level: 88, color: 'bg-cyan-500' },
    { name: 'Node.js', level: 85, color: 'bg-green-500' },
    { name: 'Git', level: 92, color: 'bg-orange-500' }
  ];

  return (
    <div className="min-h-screen bg-gradient-to-br from-gray-900 via-purple-900 to-black text-white overflow-hidden relative">
      {/* Animated Background Particles */}
      {particles.map(particle => (
        <div
          key={particle.id}
          className="absolute rounded-full bg-purple-500 opacity-30 animate-pulse"
          style={{
            left: `${particle.x}%`,
            top: `${particle.y}%`,
            width: `${particle.size}px`,
            height: `${particle.size}px`,
            animation: `float ${particle.duration}s ease-in-out infinite`
          }}
        />
      ))}

      <style>{`
        @keyframes float {
          0%, 100% { transform: translateY(0px) rotate(0deg); }
          50% { transform: translateY(-20px) rotate(180deg); }
        }
        @keyframes dragonFly {
          0%, 100% { transform: translateY(0px) rotate(-5deg); }
          50% { transform: translateY(-30px) rotate(5deg); }
        }
        @keyframes glow {
          0%, 100% { box-shadow: 0 0 20px rgba(168, 85, 247, 0.5); }
          50% { box-shadow: 0 0 40px rgba(168, 85, 247, 0.8), 0 0 60px rgba(168, 85, 247, 0.4); }
        }
        @keyframes slideIn {
          from { transform: translateX(-100%); opacity: 0; }
          to { transform: translateX(0); opacity: 1; }
        }
        .dragon-container {
          animation: dragonFly 4s ease-in-out infinite;
        }
        .glow-text {
          text-shadow: 0 0 10px rgba(168, 85, 247, 0.8), 0 0 20px rgba(168, 85, 247, 0.6);
        }
        .card-hover {
          transition: all 0.3s ease;
        }
        .card-hover:hover {
          transform: translateY(-10px) scale(1.05);
        }
      `}</style>

      {/* Flying Dragon */}
      <div 
        className="fixed top-20 right-10 z-50 dragon-container pointer-events-none"
        style={{
          transform: `translate(${dragonPos.x}px, ${dragonPos.y}px)`
        }}
      >
        <div className="relative">
          <div className="text-8xl animate-pulse">🐉</div>
          <div className="absolute top-0 left-0 text-8xl opacity-50 blur-sm">🐉</div>
        </div>
      </div>

      {/* Header Section */}
      <div className="relative z-10 pt-20 pb-10">
        <div className="max-w-6xl mx-auto px-6">
          <div className="text-center mb-12">
            <div className="inline-block relative mb-6">
              <div className="absolute inset-0 bg-purple-600 blur-3xl opacity-50 animate-pulse"></div>
              <h1 className="text-7xl md:text-9xl font-black glow-text relative animate-pulse">
                AUFA RAFIF ZAIDAN
              </h1>
            </div>
            <div className="flex items-center justify-center gap-4 text-3xl md:text-4xl mb-6">
              <Skull className="w-10 h-10 text-red-500 animate-pulse" />
              <span className="font-bold bg-gradient-to-r from-purple-400 to-pink-400 bg-clip-text text-transparent">
                CODE NECROMANCER
              </span>
              <Skull className="w-10 h-10 text-red-500 animate-pulse" />
            </div>
            <p className="text-xl text-gray-300 max-w-2xl mx-auto mb-8">
              Summoning digital demons and slaying bugs in the darkest depths of the code realm. 
              Forging legendary applications with fire and fury.
            </p>
            <div className="flex gap-4 justify-center flex-wrap">
              <button className="px-8 py-4 bg-gradient-to-r from-red-600 to-purple-600 rounded-lg font-bold text-lg hover:scale-110 transition-transform shadow-lg hover:shadow-purple-500/50">
                <div className="flex items-center gap-2">
                  <Flame className="w-5 h-5" />
                  HIRE ME
                </div>
              </button>
              <button className="px-8 py-4 bg-gradient-to-r from-blue-600 to-cyan-600 rounded-lg font-bold text-lg hover:scale-110 transition-transform shadow-lg hover:shadow-blue-500/50">
                <div className="flex items-center gap-2">
                  <GitBranch className="w-5 h-5" />
                  GITHUB
                </div>
              </button>
            </div>
          </div>

          {/* Stats Grid */}
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-16">
            {stats.map((stat, idx) => (
              <div
                key={idx}
                className="card-hover relative group"
                onMouseEnter={() => setHoveredCard(idx)}
                onMouseLeave={() => setHoveredCard(null)}
              >
                <div className={`absolute inset-0 bg-gradient-to-br ${stat.color} opacity-20 rounded-xl blur-xl group-hover:opacity-40 transition-opacity`}></div>
                <div className="relative bg-black/50 backdrop-blur-sm border-2 border-purple-500/30 rounded-xl p-6 hover:border-purple-500 transition-all">
                  <stat.icon className={`w-12 h-12 mb-4 ${hoveredCard === idx ? 'animate-bounce' : ''}`} />
                  <div className="text-4xl font-black mb-2 bg-gradient-to-r from-purple-400 to-pink-400 bg-clip-text text-transparent">
                    {stat.value}
                  </div>
                  <div className="text-gray-400 font-semibold">{stat.label}</div>
                </div>
              </div>
            ))}
          </div>

          {/* Skills Section */}
          <div className="mb-16">
            <div className="flex items-center gap-4 mb-8">
              <Zap className="w-8 h-8 text-yellow-500" />
              <h2 className="text-4xl font-black glow-text">LEGENDARY POWERS</h2>
              <Zap className="w-8 h-8 text-yellow-500" />
            </div>
            <div className="bg-black/50 backdrop-blur-sm border-2 border-purple-500/30 rounded-xl p-8">
              {skills.map((skill, idx) => (
                <div key={idx} className="mb-6 last:mb-0">
                  <div className="flex justify-between mb-2">
                    <span className="font-bold text-lg">{skill.name}</span>
                    <span className="text-purple-400 font-bold">{skill.level}%</span>
                  </div>
                  <div className="h-4 bg-gray-800 rounded-full overflow-hidden border border-purple-500/30">
                    <div
                      className={`h-full ${skill.color} transition-all duration-1000 ease-out relative`}
                      style={{ width: `${skill.level}%` }}
                    >
                      <div className="absolute inset-0 bg-white/20 animate-pulse"></div>
                    </div>
                  </div>
                </div>
              ))}
            </div>
          </div>

          {/* Battle Cry Section */}
          <div className="text-center">
            <div className="inline-block bg-gradient-to-r from-red-600 via-purple-600 to-blue-600 p-1 rounded-xl mb-8">
              <div className="bg-black px-8 py-6 rounded-lg">
                <Shield className="w-12 h-12 mx-auto mb-4 text-yellow-500 animate-pulse" />
                <p className="text-2xl font-bold italic">
                  "I don't write code. I summon it from the void."
                </p>
              </div>
            </div>
          </div>

          {/* Footer */}
          <div className="text-center mt-16 pb-8">
            <div className="flex items-center justify-center gap-3 text-xl mb-4">
              <Star className="w-6 h-6 text-yellow-500 animate-spin" />
              <span className="font-bold">May your builds be successful and your bugs be few</span>
              <Star className="w-6 h-6 text-yellow-500 animate-spin" />
            </div>
            <p className="text-gray-500">© 2024 Aufa Rafif Zaidan - All Rights Reserved</p>
          </div>
        </div>
      </div>
    </div>
  );
}