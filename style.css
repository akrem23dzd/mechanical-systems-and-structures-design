document.documentElement.classList.add("js-enabled");

const siteHeader = document.querySelector(".site-header");
const navToggle = document.querySelector(".nav-toggle");
const navMenu = document.querySelector(".nav-links");
const navLinks = document.querySelectorAll('.nav-links a[href^="#"]');
const backToTopButton = document.querySelector(".back-to-top");
const revealItems = document.querySelectorAll(".reveal");
const sections = document.querySelectorAll("main section[id]");
const projectToggles = document.querySelectorAll("[data-project-toggle]");
const currentYear = document.querySelector("#current-year");
const prefersReducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)");

const closeMenu = () => {
  siteHeader.classList.remove("menu-open");
  navToggle.setAttribute("aria-expanded", "false");
};

if (currentYear) {
  currentYear.textContent = new Date().getFullYear();
}

if (navToggle && navMenu) {
  navToggle.addEventListener("click", () => {
    const isOpen = siteHeader.classList.toggle("menu-open");
    navToggle.setAttribute("aria-expanded", String(isOpen));
  });

  navLinks.forEach((link) => {
    link.addEventListener("click", () => {
      closeMenu();
    });
  });

  window.addEventListener("resize", () => {
    if (window.innerWidth > 840) {
      closeMenu();
    }
  });

  document.addEventListener("keydown", (event) => {
    if (event.key === "Escape") {
      closeMenu();
    }
  });
}

const handleScrollState = () => {
  const shouldElevateHeader = window.scrollY > 20;
  const shouldShowBackToTop = window.scrollY > 520;

  siteHeader.classList.toggle("is-scrolled", shouldElevateHeader);
  backToTopButton.classList.toggle("is-visible", shouldShowBackToTop);
};

handleScrollState();
window.addEventListener("scroll", handleScrollState, { passive: true });

if (backToTopButton) {
  backToTopButton.addEventListener("click", () => {
    window.scrollTo({ top: 0, behavior: prefersReducedMotion.matches ? "auto" : "smooth" });
  });
}

if (!prefersReducedMotion.matches) {
  const revealObserver = new IntersectionObserver(
    (entries, observer) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) {
          return;
        }

        entry.target.classList.add("is-visible");
        observer.unobserve(entry.target);
      });
    },
    {
      threshold: 0.15,
      rootMargin: "0px 0px -10% 0px",
    }
  );

  revealItems.forEach((item) => revealObserver.observe(item));
} else {
  revealItems.forEach((item) => item.classList.add("is-visible"));
}

const setActiveLink = (id) => {
  navLinks.forEach((link) => {
    const matches = link.getAttribute("href") === `#${id}`;
    link.classList.toggle("is-active", matches);
  });
};

const sectionObserver = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        setActiveLink(entry.target.id);
      }
    });
  },
  {
    threshold: 0.45,
    rootMargin: "-20% 0px -45% 0px",
  }
);

sections.forEach((section) => sectionObserver.observe(section));

projectToggles.forEach((button) => {
  const targetId = button.getAttribute("aria-controls");
  const details = targetId ? document.getElementById(targetId) : null;

  if (!details) {
    return;
  }

  button.addEventListener("click", () => {
    const isExpanded = button.getAttribute("aria-expanded") === "true";
    button.setAttribute("aria-expanded", String(!isExpanded));
    button.textContent = isExpanded ? "View Details" : "Hide Details";
    details.hidden = isExpanded;
  });
});
