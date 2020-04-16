
all: 1 2 3 4 5 6 7 8 9 10 11

S1="Tema 1 - Introducción a Arduino.md"
F1="Tema 1 - Introducción a Arduino.docx"
S2="Tema 2 - Hardware de  Arduino.md"
F2="Tema 2 - Hardware de  Arduino.docx"
S3="Tema 3 - Programación de  Arduino.md"
F3="Tema 3 - Programación de  Arduino.docx"
S4="Tema 4 - Controlando el mundo físico con Arduino.md"
F4="Tema 4 - Controlando el mundo físico con Arduino.docx"
S5="Tema 5 - Programacion Avanzada.md"
F5="Tema 5 - Programación Avanzada.docx"
S6="Tema 6.1 - Uso de pantallas.md"
F6="Tema 6 - Uso de pantallas.docx"
S7="Tema 7.2 - Lectura de sensores.md"
F7="Tema 7 - Lectura de sensores.docx"
F8="Tema 8 - Ampliando Arduino.docx"
S8="Tema 8.0 - Expandiendo Arduino.md"
S9="Tema 9 - Control de potencia.md"
F9="Tema 9 - Control de potencia y motores.docx"
S10="Tema 10 - Comunicaciones.md"
F10="Tema 10 - Comunicaciones.docx"
S11="Tema 11 - Procesado de datos desde el PC.md"
F11="Tema 11 - Procesado de datos desde el PC.docx"

1:
	pandoc --latex-engine=xelatex   \
					-V papersize:a4paper    \
					--template=./LaTeX_ES.latex    \
					-o  $(F1)  \
					Cabecera.md        \
					Cabecera_latex.md \
					$(S1)
2:
	pandoc --latex-engine=xelatex   \
					-V papersize:a4paper    \
					--template=./LaTeX_ES.latex    \
					-o $(F2)     \
					Cabecera.md        \
					Cabecera_latex.md  \
					$(S2)

3:
	pandoc --latex-engine=xelatex \
					--from=markdown \
					-V papersize:a4paper \
					--template=./LaTeX_ES.latex \
					-o $(F3) \
					Cabecera.md     \
					Cabecera_latex.md \
					$(S3)
4:
	pandoc --latex-engine=xelatex       \
					-V papersize:a4paper        \
					--template=./LaTeX_ES.latex \
					-o $(F4) \
					Cabecera.md           \
					Cabecera_latex.md \
					$(S4) \
					"Tema 4 - sensores.md" \
					"Tema 4 - Proyectos sencillos con sensores.md"


5:
	pandoc --latex-engine=xelatex       \
					-V papersize:a4paper        \
					--template=./LaTeX_ES.latex \
					-o $(F5) \
					Cabecera.md           \
					Cabecera_latex.md \
					$(S5) \
					"Tema 5.1 - Programacion_C++.md" \
					"Tema 5.2 - Tiempos.md" \
					"Tema 5.3 - ProcesoCompilacion.md" \
					"Tema 5.4 - Interrupciones.md" \
					"Tema 5.5 - UsoAvanzadoPuertos.md"

6:
	pandoc --latex-engine=xelatex       \
					-V papersize:a4paper        \
					--template=./LaTeX_ES.latex \
					-o $(F6) \
					Cabecera.md           \
					Cabecera_latex.md \
					$(S6) \
					"Tema 6.2 - Proyectos sencillos con pantallas.md"

7:
	pandoc --latex-engine=xelatex       \
					-V papersize:a4paper        \
					--template=./LaTeX_ES.latex \
					-o $(F7) \
					Cabecera.md           \
					Cabecera_latex.md \
					"Tema 7.1 - Electronica.md" \
					$(S7)

8:
	pandoc --latex-engine=xelatex       \
					-V papersize:a4paper        \
					--template=./LaTeX_ES.latex \
					-o $(F8) \
					Cabecera.md           \
					Cabecera_latex.md \
					$(S8) \
					"Tema 8.1 - ADC.md" \
					"Tema 8.2 - DAC.md" \
					"Tema 8.3 - Interrupciones Hardware.md"

9:
	pandoc --latex-engine=xelatex       \
					-V papersize:a4paper        \
					--template=./LaTeX_ES.latex \
					-o $(F9) \
					Cabecera.md           \
					Cabecera_latex.md \
					$(S9) \
					T9_motores.md

10:
	pandoc --latex-engine=xelatex       \
					-V papersize:a4paper        \
					--template=./LaTeX_ES.latex \
					-o $(F10) \
					Cabecera.md           \
					Cabecera_latex.md \
					$(S10) \
					T10_Serie.md \
					T10_Bluetooth.md \
					T10_Infrarrojos.md \
					T10_comunicaciones.md \
					T10_wifi.md \
					T10_esp8266.md \
					T10_comunicaciones_radio.md \
					T10_gps.md \
					T10_rfids.md

11:
	pandoc --latex-engine=xelatex       \
					-V papersize:a4paper        \
					--template=./LaTeX_ES.latex \
					-o $(F11) \
					Cabecera.md           \
					Cabecera_latex.md \
					$(S11)

clean:
	rm $(F1) $(F2) $(F3) $(F4) $(F5) $(F6) $(F7) $(F8) $(F9) $(F10) $(F11)

cp:
	cp $(F1) $(F2) $(F3) $(F4) $(F5) $(F6) $(F7) $(F8) $(F9) $(F10) $(F11) /home/javacasm/Dropbox/Cursos/ArduinoExpertoDesde0DE_2020/TEMARIO

push:
	git commit -m "update" $(S1);
	git commit -m "update" $(S2);
	git commit -m "update" $(S3);
	git commit -m "update" $(S4) T4_sensores.md;
	git commit -m "update" $(S5) T5_*.md;
	git commit -m "update" $(S6);
	git commit -m "update" $(S7) T7_*.md;
	git commit -m "update" $(S8) T8_*.md;
	git commit -m "update" $(S9) T9_*.md;
	git commit -m "update" $(S10) T10_*.md;
	git commit -m "update" $(S11);
	git push;
