<!DOCTYPE html><html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Malla Enfermería</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #0a1a2f;
      color: #fff;
      padding: 20px;
    }
    h1 {
      text-align: center;
      color: #9ecfff;
    }
    .year {
      margin-bottom: 40px;
    }
    h2 {
      color: #6ba8e5;
    }
    .semester {
      display: flex;
      flex-direction: row;
      gap: 15px;
      flex-wrap: wrap;
      margin-bottom: 15px;
    }
    .course {
      background-color: #133b5c;
      border: 1px solid #1d5b8f;
      border-radius: 10px;
      padding: 10px 15px;
      cursor: pointer;
      transition: background-color 0.3s, text-decoration 0.3s;
      flex: 1 1 250px;
    }
    .course.completed {
      text-decoration: line-through;
      background-color: #2a5173;
      color: #b0cfe5;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <h1>Malla de la Carrera de Enfermería</h1>  <div id="malla"></div>  <script>
    const cursos = [
      {
        year: 1,
        semesters: [
          {
            name: "1° Semestre",
            courses: [
              { id: "bio", name: "Fundamentos de Biología y Genética Humana" },
              { id: "quimica", name: "Bases Químicas y Bioquímicas de la vida" },
              { id: "gest1", name: "Gestión del Cuidado en Enfermería 1" },
              { id: "edu1", name: "Educación en Enfermería 1" },
              { id: "ing1", name: "Inglés 1" },
              { id: "hab1", name: "Habilidades Académicas 1" },
            ],
          },
          {
            name: "2° Semestre",
            courses: [
              { id: "morf", name: "Morfología Micro y Macroscópica", req: ["bio"] },
              { id: "microbio", name: "Microbiología y Agentes Infecciosos", req: ["quimica"] },
              { id: "gest2", name: "Gestión del Cuidado en Enfermería 2", req: ["gest1"] },
              { id: "edu2", name: "Educación en Enfermería 2", req: ["edu1"] },
              { id: "hab2", name: "Habilidades Académicas 2", req: ["hab1"] },
              { id: "ing2", name: "Inglés 2", req: ["ing1"] },
            ],
          },
        ],
      },
      {
        year: 2,
        semesters: [
          {
            name: "3° Semestre",
            courses: [
              { id: "fisio1", name: "Fisiología y Fisiopatología de Sistemas 1", req: ["morf"] },
              { id: "gest3", name: "Gestión del Cuidado en Enfermería 3", req: ["gest2"] },
              { id: "saludpub", name: "Enfermería en Salud Pública y Determinantes Sociales", req: ["edu2"] },
              { id: "antro", name: "Socioantropología en la Humanización del Cuidado" },
              { id: "ing3", name: "Inglés 3", req: ["ing2"] },
              { id: "etica", name: "Ética y Ciudadanía" },
              { id: "prac1", name: "Práctica Integrada en Enfermería 1", req: ["gest2"] },
            ],
          },
          {
            name: "4° Semestre",
            courses: [
              { id: "fisio2", name: "Fisiología y Fisiopatología de Sistemas 2", req: ["fisio1"] },
              { id: "farma", name: "Farmacología Clínica Fundamental", req: ["microbio"] },
              { id: "servsalud", name: "Gestión en Servicio de Salud", req: ["gest3"] },
              { id: "tic", name: "Matemáticas, TICs en Informática" },
              { id: "ing4", name: "Inglés 4", req: ["ing3"] },
              { id: "rsu", name: "Responsabilidad Social Universitaria", req: ["etica"] },
              { id: "prac2", name: "Práctica Integrada en Enfermería 2", req: ["gest3", "prac1"] },
            ],
          },
        ],
      },
      {
        year: 3,
        semesters: [
          {
            name: "5° Semestre",
            courses: [
              { id: "metodoinv", name: "Metodología de la Investigación y Bioética", req: ["tic"] },
              { id: "com1", name: "Gestión del Cuidado en Comunidades 1", req: ["saludpub"] },
              { id: "adulto1", name: "Gestión del Cuidado en el Adulto 1", req: ["gest3", "farma", "fisio2"] },
              { id: "mayor", name: "Gestión del Cuidado en la Persona Mayor", req: ["gest3", "farma", "fisio2"] },
              { id: "calidad", name: "Calidad y Gestión en el Cuidado", req: ["servsalud"] },
              { id: "prac3", name: "Práctica Integrada en Enfermería 3", req: ["farma", "fisio2", "prac2"] },
            ],
          },
          {
            name: "6° Semestre",
            courses: [
              { id: "proyin1", name: "Proyecto de Investigación 1", req: ["metodoinv"] },
              { id: "com2", name: "Gestión del Cuidado en Comunidades 2", req: ["com1"] },
              { id: "adulto2", name: "Gestión del Cuidado en el Adulto 2", req: ["adulto1"] },
              { id: "mujer", name: "Gestión del Cuidado en la Mujer", req: ["farma", "fisio2"] },
              { id: "elec1", name: "Electivo Formación General 1" },
              { id: "prac4", name: "Práctica Integrada en Enfermería 4", req: ["com1"] },
            ],
          },
        ],
      },
      {
        year: 4,
        semesters: [
          {
            name: "7° Semestre",
            courses: [
              { id: "proyin2", name: "Proyecto de Investigación 2", req: ["proyin1"] },
              { id: "com3", name: "Gestión del Cuidado en Comunidades 3", req: ["com2"] },
              { id: "nino1", name: "Gestión del Cuidado en el Niño y Adolescente 1", req: ["mujer"] },
              { id: "urgencias", name: "Gestión del Cuidado en Urgencias", req: ["adulto2"] },
              { id: "mental1", name: "Gestión del Cuidado en Salud Mental 1", req: ["adulto2"] },
              { id: "prac5", name: "Práctica Integrada en Enfermería 5", req: ["mujer"] },
            ],
          },
          {
            name: "8° Semestre",
            courses: [
              { id: "intercultural", name: "Cuidados de la Salud en Interculturalidad", req: ["com3"] },
              { id: "nino2", name: "Gestión del Cuidado en el Niño y Adolescente 2", req: ["nino1"] },
              { id: "mental2", name: "Gestión del Cuidado en Salud Mental 2", req: ["mental1"] },
              { id: "elec2", name: "Electivo Formación General 2" },
              { id: "prac6", name: "Práctica Integrada en Enfermería 6", req: ["urgencias"] },
            ],
          },
        ],
      },
      {
        year: 5,
        semesters: [
          {
            name: "9° Semestre",
            courses: [
              { id: "pracpro1", name: "Práctica Profesional en Enfermería 1", req: ["calidad", "adulto1", "com1", "mayor", "metodoinv", "prac3", "elec1", "adulto2", "com2", "mujer", "prac5", "proyin1", "nino1", "mental1", "com3", "urgencias", "proyin2", "nino2", "mental2", "intercultural", "elec2", "prac6"] },
            ],
          },
          {
            name: "10° Semestre",
            courses: [
              { id: "pracpro2", name: "Práctica Profesional en Enfermería 2", req: ["pracpro1"] },
              { id: "profund", name: "Electivo de Profundización", req: ["pracpro1"] },
            ],
          },
        ],
      }
    ];

    const container = document.getElementById("malla");
    const completed = JSON.parse(localStorage.getItem("completed") || "[]");

    function canShow(course) {
      if (!course.req) return true;
      return course.req.every((id) => completed.includes(id));
    }

    function render() {
      container.innerHTML = "";
      cursos.forEach((año) => {
        const yearDiv = document.createElement("div");
        yearDiv.className = "year";
        yearDiv.innerHTML = `<h2>${año.year}° Año</h2>`;
        año.semesters.forEach((semestre) => {
          const semDiv = document.createElement("div");
          semDiv.innerHTML = `<h3>${semestre.name}</h3>`;
          semDiv.className = "semester";
          semestre.courses.forEach((curso) => {
            const btn = document.createElement("div");
            btn.className = `course${completed.includes(curso.id) ? " completed" : ""}${canShow(curso) ? "" : " hidden"}`;
            btn.textContent = curso.name;
            btn.onclick = () => {
              const idx = completed.indexOf(curso.id);
              if (idx > -1) completed.splice(idx, 1);
              else completed.push(curso.id);
              localStorage.setItem("completed", JSON.stringify(completed));
              render();
            };
            semDiv.appendChild(btn);
          });
          yearDiv.appendChild(semDiv);
        });
        container.appendChild(yearDiv);
      });
    }

    render();
  </script></body>
</html>
