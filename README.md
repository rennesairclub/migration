# Migration de site

1. Installer Wordpress

2. Mettre à jours

3. Installer les plugins 
    - rac-customization
    - rac-social-media
    - Contact Form 7

4. Menu Outils>Importer, installer l'importeur Wordpress

5. Menu Apparence>Widget
    A - Pieds de page:
        - Calendar => "Évènements"

6. Menu Apparence>Thème, installer le theme
    - sudo unzip radcliffe-2-wpcom-2-0-6.zip
    - sudo chown -R www-data:www-data radcliffe-2-wpcom
    - Activer le thème

7. Créer les 3 comptes:
    - Antoine
    - Danielle
    - Cyrille

8. Menu Outils>Importer, import des données wordpress.2020-11-10.xml
    - remplacer les URLs dans le fichier si besoin
    - Wordpress>Lancer l'outil d'importation
    - Sélectionner le xml et valider
    - Affecter ou créer les utilisateurs
    - cocher la case "Téléverser et importer les fichiers joints"

9. Dans le menu Apparence>Personnaliser
    A - Identité du site
        * Logo => capture-decc81cran-2020-09-20-acc80-20.37.24.png
        * Ajuster la taille du Logo
        * Effacer le titre et le slogan
        * décocher "Afficher le titre et le slogan"
        * Icône du site => capture-decc81cran-2020-10-08-acc80-00.22.18.png
        * Publier
    B. Information de contact
        * Dans le pied de page
        * Adresse: 50 Rue Jules Vallès . 35136 Saint-Jacques-de-la-Lande
        * Téléphone: 02 99 31 69 91
        * Publier
    C. Style Packs
        * Active Style (le premier)
    D. Menus
        * Entête => Onglet
        * Social Menu => Social
        * Dans le menu Social, changer 
            - 'facebook' par '<span class="dashicons dashicons-facebook"></span>'
            - 'twitter' par '<span class="dashicons dashicons-twitter"></span>'
            - 'instagram' par '<span class="dashicons dashicons-instagram"></span>'
        * Publier
    E. Réglage de la page d'accueil
        * Une page static => "Bienvenue!"

10. Editer la page "Plan d'accès"
    <div class="googlemaps">
        <iframe width="600" height="450" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d10666.141300171235!2d-1.7341378!3d48.0613091!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0:0x770a1d3f44118055!2sRennes%20Air%20Club!5e0!3m2!1sfr!2sfr!4v1600623941967!5m2!1sfr!2sfr"></iframe>
    </div>

11. Jouer la requête SQL:
    UPDATE wp_posts SET guid=REPLACE(guid, 'https://rennesairclub.wordpress.com', 'https://rennes-air-club.noopy.fr') WHERE guid like 'https://rennesairclub.wordpress.com%';

12. Modifier le formulaire de contact:
    A. formulaire
        <label class="required"> Nom, Prénom <span class="note">(obligatoire)</span></label>
        [text* nom] 

        <label class="required"> E-mail <span class="note">(obligatoire)</span></label>
            [email* email]

        <label class="required"> Numéro de téléphone <span class="note">(obligatoire)</span></label>
            [text* telephone]

        <label class="required"> Rensignements souhaités <span class="note">(obligatoire)</span></label>
        [select objet "Vol d'initiation" "Vol de découverte" "Formation" "Adhésion annuelle" "Devenir bénévole" "Renouvellement PPL" "Autre"]

        <label class="required"> Message <span class="note">(obligatoire)</span></label>
            [textarea message]

        [submit "Envoyer"]
    
    B. E-Mail
        Pour                        [_site_admin_email]
        De                          [_site_title] <wordpress@rennes-air-club.noopy.fr>
        Objet                       [_site_title] "[objet]"
        En-têtes additionnelles	    Reply-To: [email]
        Corps du message	        De : [name] <[email]> ([telephone])
                                    Objet : [objet]
                                    
                                    Corps du message :
                                    [message]

                                    -- 
                                    Cet e-mail a été envoyé via le formulaire de contact de [_site_title] ([_site_url])
    C. Modifier la page "Romeo Alpha Charlie à votre écoute" pour insérer le formulaire 

13. Dans le menu Apparence>Personnaliser, ajouter le CSS
        div.site-info {
        display: none !important;
        }

        header#masthead {
        margin: 0;
        padding-top: 0;
        border-top: 0;
        }

        div.googlemaps {
        text-align: center;
        }

        form.wpcf7-form label span.note {
        font-size: 0.8em;
            font-weight: normal;
        }

        form.wpcf7-form label {
            font-weight: bold;
            font-family: raleway;
        }

14. Faire une passe sur toutes les pages pour changer les url absolues en URL relatives