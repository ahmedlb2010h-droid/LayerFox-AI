LayerFox AI v0.3 — integration starter
=======================================

What this package contains
- index.html: mobile-first LayerFox UI. It does not show the upstream AI website.
- backend/app.py: FastAPI backend that calls the See-through Space through gradio_client.
- backend/requirements.txt: backend dependencies.

Important honesty note
----------------------
This is an integration starter, not a deployed live service. The upstream Space's
API endpoint name and parameter schema can change. Before it will process images,
verify the current API:
  from gradio_client import Client
  client = Client("24yearsold/see-through-demo")
  print(client.view_api())

Then update SEE_THROUGH_API_NAME and the `client.predict(...)` arguments in app.py.
The backend currently returns the layered PSD. It does NOT yet create Alight Motion
XML. A real XML sample exported by Alight Motion is needed to inspect its structure
and test compatibility.

How to run backend locally (computer or cloud Python host)
----------------------------------------------------------
1. Install Python 3.11+.
2. In backend directory:
   pip install -r requirements.txt
3. Start:
   uvicorn app:app --host 0.0.0.0 --port 7860
4. Host index.html on HTTPS/static hosting.
5. Set localStorage key `layerfox_backend_url` to the backend URL in the browser console:
   localStorage.setItem('layerfox_backend_url', 'https://YOUR-BACKEND-URL')
   (This is a temporary developer setting, not intended for end users.)
6. Verify CORS ALLOWED_ORIGINS is set to the site's origin before public use.

Free hosting caveat
-------------------
Free services have sleep, runtime, GPU quota, and request limits. The AI Space's
own free quota is controlled by its provider. This project does not bypass limits.
Do not expose private API tokens in frontend JavaScript.

Next steps
----------
- Verify the exact Gradio API signature.
- Deploy backend to a free host that permits the dependencies and outbound calls.
- Add PSD-to-PNG layer extraction with original canvas placement.
- Inspect an authentic Alight Motion XML export and implement/test XML generation.
