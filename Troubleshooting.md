Troubleshooting Summary for Your Practica2 Issue
Problem:
Practica2 folder is treated as a Git submodule.

You get errors trying to add files inside it.

Submodule seems uninitialized or broken (fatal: No url found for submodule path 'Practica2' in .gitmodules).

Step-by-step troubleshooting:

Check if Practica2 is a submodule

git submodule status

If Practica2 is listed, it’s a submodule.

Try to initialize and update submodules

git submodule update --init --recursive

If you get the error about missing URL in .gitmodules, the submodule config is broken or missing.

Inspect .gitmodules file

Check if .gitmodules exists and contains a valid URL for Practica2.

If missing or incorrect, Git can’t fetch submodule data.

Decide: keep or remove the submodule?

If you want Practica2 to be a proper submodule (separate repo linked inside your repo), fix .gitmodules and run update commands again.

If you don’t want Practica2 as a submodule, remove it as submodule and add it as a normal folder:

Remove the broken submodule:

git submodule deinit -f Practica2

git rm --cached Practica2

rm -rf .git/modules/Practica2

rm .gitmodules  # if this file only had Practica2 or is broken

git commit -m "Remove Practica2 submodule"

Add Practica2 as a normal folder:

Ensure the folder and files are present.

git add Practica2

git commit -m "Add Practica2 as normal folder"

