# Sistema de Badges "NEW" - Guía de Uso

## 📋 Propósito
Este sistema permite agregar badges "NEW" a secciones modificadas que se auto-ocultan automáticamente después de **3 días**.

## 🎯 Ubicación de los Badges

Los badges "NEW" aparecen en **dos lugares**:

1. **Sidebar de navegación** - Al lado del nombre del link
2. **Card header** - En la cabecera de la sección (opcional)

---

## ✨ Cómo Agregar un Badge "NEW" a una Nueva Sección

### Paso 1: Agregar el Badge en el Sidebar

Encuentra el enlace de navegación en el sidebar y agrega el badge:

```html
<!-- ANTES -->
<a href="#mi-seccion" class="nav-link">
    <i class="fas fa-icon"></i> 
    <span>Mi Sección</span>
</a>

<!-- DESPUÉS -->
<a href="#mi-seccion" class="nav-link">
    <i class="fas fa-icon"></i> 
    <span>Mi Sección<span class="nav-badge-new" id="mi-seccion-new-badge">NEW</span></span>
</a>
```

**⚠️ Importante**: 
- El `id` debe seguir el patrón: `[nombre-seccion]-new-badge`
- El badge se coloca DENTRO del `<span>` que contiene el texto

### Paso 2: Agregar el Badge en el Card Header (Opcional)

En la sección misma, agrega el badge al header:

```html
<article class="card span-2" id="mi-seccion">
    <div class="card-header">
        <h2 class="card-title">
            <span class="card-icon"><i class="fas fa-icon"></i></span>
            Mi Sección
        </h2>
        <span class="card-badge">CATEGORÍA</span>
        <!-- ⬇️ AGREGAR ESTE BADGE -->
        <span class="card-badge" style="background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%); color: white; margin-left: 0.5rem;" id="mi-seccion-card-badge">NEW</span>
    </div>
    ...
</article>
```

### Paso 3: Registrar el Badge en el JavaScript

Al final del archivo `index.html`, busca el script de auto-ocultamiento y agrega tu badge al array:

```javascript
// Auto-hide NEW badges after 3 days
(function() {
    const THREE_DAYS = 3 * 24 * 60 * 60 * 1000;
    const currentDate = new Date().getTime();
    
    const badges = [
        {
            ids: ['comparativas-new-badge'],
            launchDate: new Date('2026-02-09').getTime()
        },
        {
            ids: ['ciclo-vida-new-badge', 'ciclo-vida-card-badge'],
            launchDate: new Date('2026-02-09').getTime()
        },
        // ⬇️ AGREGAR TU NUEVO BADGE AQUÍ
        {
            ids: ['mi-seccion-new-badge', 'mi-seccion-card-badge'], // Ambos IDs
            launchDate: new Date('YYYY-MM-DD').getTime() // Fecha de la modificación
        }
    ];
    
    badges.forEach(badgeGroup => {
        const timeSinceLaunch = currentDate - badgeGroup.launchDate;
        if (timeSinceLaunch > THREE_DAYS) {
            badgeGroup.ids.forEach(id => {
                const element = document.getElementById(id);
                if (element) {
                    element.style.display = 'none';
                }
            });
        }
    });
})();
```

**⚠️ Importante sobre la fecha**: 
- Usa la fecha **actual** cuando agregues el badge
- Formato: `'YYYY-MM-DD'` (ej: `'2026-02-09'`)
- El badge desaparecerá automáticamente 3 días después

---

## 📝 Ejemplo Completo

Imagina que modificaste la sección de "Seguridad" el 10 de febrero de 2026:

### 1. Sidebar:
```html
<a href="#segurity" class="nav-link">
    <i class="fas fa-shield-halved"></i> 
    <span>Seguridad<span class="nav-badge-new" id="seguridad-new-badge">NEW</span></span>
</a>
```

### 2. Card Header:
```html
<div class="card-header">
    <h2 class="card-title">
        <span class="card-icon"><i class="fas fa-shield-halved"></i></span>
        Seguridad
    </h2>
    <span class="card-badge" style="background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%); color: white; margin-left: 0.5rem;" id="seguridad-card-badge">NEW</span>
</div>
```

### 3. JavaScript:
```javascript
const badges = [
    // ... badges anteriores ...
    {
        ids: ['seguridad-new-badge', 'seguridad-card-badge'],
        launchDate: new Date('2026-02-10').getTime()
    }
];
```

---

## 🔧 Mantenimiento

### Ver cuándo expira un badge:

```javascript
const launchDate = new Date('2026-02-09');
const expirationDate = new Date(launchDate.getTime() + (3 * 24 * 60 * 60 * 1000));
console.log(`Badge expira el: ${expirationDate.toLocaleDateString()}`);
```

### Cambiar la duración de los badges:

Si en el futuro quieres cambiar de 3 días a otro período, modifica:

```javascript
const THREE_DAYS = 3 * 24 * 60 * 60 * 1000; // ⬅️ Cambiar el número aquí
```

Por ejemplo, para 5 días:
```javascript
const FIVE_DAYS = 5 * 24 * 60 * 60 * 1000;
```

---

## 📊 Badges Activos Actualmente

| Sección | IDs de Badges | Fecha de Lanzamiento | Fecha de Expiración |
|---------|--------------|---------------------|---------------------|
| Comparativas | `comparativas-new-badge` | 2026-02-09 | 2026-02-12 |
| Ciclo de Vida | `ciclo-vida-new-badge`, `ciclo-vida-card-badge` | 2026-02-09 | 2026-02-12 |

---

## ✅ Checklist para Agregar un Badge

- [ ] Agregar badge en el sidebar con ID único
- [ ] (Opcional) Agregar badge en el card header con ID único
- [ ] Registrar ambos IDs en el array de JavaScript
- [ ] Usar la fecha actual como `launchDate`
- [ ] Verificar que los IDs sean únicos y consistentes
- [ ] Probar que el badge aparezca correctamente
- [ ] Actualizar la tabla de "Badges Activos" en este documento

---

## 🎨 Estilos del Badge

El badge usa estos estilos:

**En Sidebar:**
```css
.nav-badge-new {
    display: inline-block;
    font-size: 0.6rem;
    padding: 2px 6px;
    border-radius: 8px;
    background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
    color: white;
    font-weight: 700;
    letter-spacing: 0.5px;
    margin-left: 6px;
    text-transform: uppercase;
    animation: pulse-new 2s ease-in-out infinite;
    box-shadow: 0 2px 4px rgba(245, 158, 11, 0.3);
}
```

**En Card:**
```html
style="background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%); color: white; margin-left: 0.5rem;"
```

---

**Última actualización**: 9 de febrero de 2026
