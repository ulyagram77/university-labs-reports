---
name: lab-report
description: Create and edit LaTeX reports for laboratory, practical, and calculation-and-graphics assignments in this repository. Use when the user requests a report for a specific assignment, following the repository template, clarifying objectives and tasks, and incorporating optional code and images.
---

# Report creation

All paths below are relative to the repository root, not the skill directory.
Write the report in Ukrainian unless the user requests another language.
The instructions in this skill are in English; Ukrainian report headings and
required phrases below must remain Ukrainian.

## 1. Understand the context and create the directory

Before creating a report:

1. Read `README.md`, `Makefile`, `.env.template`, and the current template
   at `src/reports/templates/lab/`, particularly `main.tex` and `settings.tex`.
2. Check the working tree and the target report if it already exists. Preserve
   unrelated changes, existing materials, and previously written content.
3. Identify the subject, assignment type, title, number, purpose, and instructor
   requirements. Never invent the context or variant. Reuse information already
   supplied in messages or materials without asking for it again.
4. Find the corresponding subject directory in `src/reports/`. Reuse its
   existing name, including Cyrillic names. If none exists, create an appropriate
   subject directory. Ask the user if the subject is ambiguous.
5. Copy the template into `src/reports/<subject>/<assignment>/` without
   overwriting an existing report. Name the directory according to the assignment
   type and number, for example `practise1`, `lab2`, or `rgz`. Do not force every
   report into the `lab<N>` naming convention.

New report layout:

```text
src/reports/<subject>/<assignment>/
├── main.tex
├── settings.tex
├── assets/
└── code/
```

Store images, plots, and illustrations in the report's `assets/` directory
and source files in its `code/` directory. Do not move them into shared
`src/code/`. Use the current template rather than legacy report structures.
Images and code are optional: these directories may remain empty.

## 2. Settings are the user's responsibility

- **Do not fill in or edit the report's `settings.tex`.** For a new report,
  leave it exactly as copied from the template; for an existing report,
  preserve its contents. The user fills in this file entirely themselves.
  Do not ask for instructor, department, or other metadata solely to fill it in.
- **Always use `PROFILE=default`.** Select another existing profile or create
  a new one only when the user explicitly requests it. Never switch automatically.
- Read `src/profiles/default/profile.tex` to understand the available macros,
  but do not change personal information, the variant, or paths without a request.
- Do not edit generated `src/settings.tex`; Make creates it.
- Do not modify `src/main.tex`, `src/base/`, classes, the template, or build
  infrastructure for an individual report without separate agreement.

## 3. Clarify content in order

Do not generate the complete report before understanding its purpose.
Follow the order below. Treat information already supplied by the user as
answered; do not ask the same questions again.

### Objective

First ask the user for the objective. If they do not have a clear objective,
ask them to explain the assignment's purpose: what they need to implement,
investigate, or learn. Then formulate the objective from their explanation.
Keep it concise: **1–2 sentences**, without generic filler.

### Tasks

Next ask for the assignment tasks if they have not already been supplied.
If the user does not supply tasks or says there are none, **omit the entire
“Завдання” section**. Do not invent tasks or leave an empty section.
Present supplied tasks individually using subsections, as in the template:

```latex
\section{Завдання}
\subsection{Перше завдання}
Текст першого завдання.
\subsection{Друге завдання}
Текст другого завдання.
```

### Optional images, code, and execution materials

**Always clarify with the user whether images and program code are needed**,
what is already available, and what they will add later. Existing or missing
files alone do not establish the user's preference.
Ask for performed steps and results if there is insufficient context.

**Both images and code are optional and independent of each other.**
A report may contain neither, only images, only code, or both. Do not require
them, fabricate them, or create empty sections just to match the template.
When the user confirms that one is unnecessary, omit its corresponding blocks,
placeholders, or appendix. Continue normally with a text-only report if needed.

Before generating content, always inspect the selected report's `code/` and
`assets/`, including nested directories. Read relevant code and inspect available
images to associate them with the correct steps. Files copied as template
examples are not evidence that the assignment has been performed.

## 4. Fill in `main.tex`

Follow the template's formatting. Include only the report body: no
`\documentclass`, preamble, `\begin{document}`, title page, or custom contents.
Use ordinary `\section`, `\subsection`, and `\subsubsection` commands;
never type heading numbers manually.

Section order:

1. Objective: `\section*{Мета}` and `\addcontentsline{toc}{section}{Мета}`.
2. Tasks: “Завдання”, only if supplied by the user.
3. Procedure: “Хід виконання”.
4. Conclusions: `\section*{Висновки}` and its explicit contents entry.
5. Appendix: “Додаток”, the final section, only when code is included.

### Procedure

Generate the procedure from the objective, supplied tasks (if any), the user's
description, available materials, and any existing procedure text.
Organize it into meaningful subsections describing the steps, methods, and
results. Do not replace explanations with a collection of images.

When images are needed, place them **at the end of their corresponding
subsection**. Use existing files from `assets/`. If the user confirms that
they will add images later, prepare figure blocks with specific descriptive
filenames, captions, and unique labels in advance. Do not add figure blocks
or placeholders when images are not needed.

For future files, check for existence so a missing image does not prevent
compilation. Adding the file should make the image appear automatically:

```latex
\begin{figure}[h!]
    \centering
    \IfFileExists{\assetsDirectory/task1-result.png}{
        \includegraphics[width=.9\textwidth]{\assetsDirectory/task1-result.png}
    }{
        \fbox{\parbox{.85\textwidth}{\centering
            Місце для зображення результату першого завдання}}
    }
    \caption{Результат виконання першого завдання}
    \label{fig:task1-result}
\end{figure}
```

Do not claim that a planned image already demonstrates a verified result.
Never invent measurements, program executions, experiments, or other evidence.
Distinguish expected results from observed results.

### Conclusions

Generate conclusions from the student's perspective, using the first person.
Preserve the template's opening **“Протягом лабораторної роботи було…”**,
then naturally continue with phrases such as “я реалізував…”,
“я дослідив…”, or “я навчився…”. For another assignment type, adjust
“лабораторної” accordingly.
Describe the specific work and skills gained in relation to the objective.
Do not attribute unsupported actions or results to the student.

### Optional code appendix

When code is included, place **all program code only at the end of the report**,
after conclusions, in a new `\section{Додаток}`. Do not put listings in the
procedure; use explanations and references to the appendix there instead.

For each supplied program source file, show its **complete code**, without
abbreviation. Precede it with “Код file.x програми:”, using the actual filename.
Use `\lstinputlisting` rather than manually duplicating file contents:

```latex
\section{Додаток}
Код solution.py програми:
\lstinputlisting[language=PythonPlus, style=colorEX]{\codeDirectory/solution.py}
```

Choose the correct listing language for each file; check available definitions
in `src/base/preambule.tex`. Include all supplied source files, including nested
paths, but not binaries, generated files, or dependencies. Do not rewrite source
code unless requested.
If code is absent or the user says it should not be included, omit the appendix
entirely. Do not create empty listings, invented code files, or code placeholders.

## 5. Validate and hand off

- Use `\assetsDirectory` and `\codeDirectory`, not absolute paths. Escape
  LaTeX special characters in prose and filenames displayed in captions.
- Check structure, file references, removal of template examples from `main.tex`,
  image-to-subsection correspondence, and appendix completeness when applicable.
  Preserve template `settings.tex`; it intentionally remains for the user.
- If `.env` is missing, it may be created from `.env.template`. Never overwrite
  an existing `.env` or disclose its contents.
- Build from the repository root using:

  ```sh
  make build REPORT='<subject>/<assignment>' PROFILE=default
  ```

  Substitute another profile only on explicit request. Repeat the build after
  heading or reference changes to update the contents. Make, Docker, and Docker
  Compose are required. Do not use plain `make`: its additional copy step
  requires `BUILDS_FOLDER`.
- Check logs and confirm the PDF was refreshed, not just Make's exit status.
  The default output is `build/main.pdf`; respect build-directory overrides.
  Inspect the PDF when possible. Never claim a successful build or visual
  inspection that was not performed.
- Do not automatically install dependencies, delete builds, or change
  infrastructure to work around errors.

Finish with a short summary of the report path, created files, validation
status, and PDF location if generated. Remind the user to fill in `settings.tex`.
List specific expected image filenames and missing materials only when the
user has agreed to provide them; do not present optional images or code as
mandatory outstanding work.
