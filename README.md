  function claimRedirect() {
  let elements = ["checkout"];

  elements = elements
    .map((name) => Array.from(document.getElementsByName(name)))
    .flat()
    .filter((e) => e && !e.phx_claimRedirect2);

  if (elements.length > 0) {
    elements.forEach((element) => {
      // Remove existing cloned version if already present
      const existingCloneId = new-${element.classList[0] || "element"};
      const existingClone = document.getElementById(existingCloneId);
      if (existingClone) {
        existingClone.remove();
        console.log(Removed existing clone with ID: ${existingCloneId});
      }

      element.style.display = "none";
      element.phx_claimRedirect2 = true;

      // Clone the element
      const clonedElement = element.cloneNode(true);
      clonedElement.id = existingCloneId;
      clonedElement.type = "submit";
      clonedElement.phx_claimRedirect2 = true;
      clonedElement.style.display = "";
      clonedElement.addEventListener("click", redirectToPage, true);

      // Replace the original with the cloned element
      element.parentNode.replaceChild(clonedElement, element);
      console.log(Added phoenix event listener to element with ID: ${clonedElement.id});
    });

    console.log("Completed claimRedirect attempt on DOM change");
  }
}
