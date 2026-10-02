# Learning-augmented robotic automation project page

Static academic project website. Edit `public/index.html` for content and `public/styles.css` for appearance; refresh the browser to see changes. No build or package installation is needed.

## Hosting

The page is served at http://192.168.0.122:8000/ on this PC's local network. This private IP is reachable by devices on the same network; internet access requires separate network routing. The IP can change if the router assigns a new address.

The user service `solder-project.service` serves only the `public/` directory. It starts with the user's service manager at login and restarts if the server crashes. It does not configure startup before login or alter the existing Apache website.

```sh
systemctl --user status solder-project.service
systemctl --user restart solder-project.service
systemctl --user stop solder-project.service
```

To serve manually while the service is stopped:

```sh
python3 -m http.server 8000 --bind 0.0.0.0 --directory public
```

To install the included service on this PC:

```sh
mkdir -p ~/.config/systemd/user
cp solder-project.service ~/.config/systemd/user/
systemctl --user daemon-reload
systemctl --user enable --now solder-project.service
```

## Assets and content

Original assets are in `source/`. The page uses the teaser and converted PNG figures in `public/assets/`. Click a figure to open it at full resolution. The learning-based components section uses a native HTML disclosure and starts collapsed. Four YouTube videos are embedded with direct playback links as a fallback.

To regenerate the figure PNGs with Poppler:

```sh
pdftoppm -png -singlefile -scale-to 2400 source/framework.pdf public/assets/framework
pdftoppm -png -singlefile -scale-to 2600 source/method.pdf public/assets/method
pdftoppm -png -singlefile -scale-to 2600 source/production_validation.pdf public/assets/production_validation
```

The abstract, affiliation, and corresponding authors match the supplied latest manuscript, `Learning_augmented_robotic_automation_for_real_world_manufacturing__2nd_revision (2).pdf`. The preprint link remains https://arxiv.org/abs/2604.22235. Captions are edited from the supplied descriptions. The favicon and header logo are copied from the `main` branch of `nrmk_ai_page`. Video IDs preserve the exact case of the supplied URLs. No external fonts, JavaScript libraries, or analytics are used.
