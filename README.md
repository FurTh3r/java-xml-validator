# Ontology Validator and Editor

A desktop application for validating, inspecting, and transforming RDF/XML and OWL ontologies through a JavaFX interface backed by CDuce.

The project was developed as part of a Bachelor's thesis in Computer Science at the University of Turin. It combines XML analysis utilities, dynamically generated CDuce programs, structural comparison, and a graphical editor in a single workflow.

## Features

- Load and format RDF/XML ontologies.
- Inspect and manage XML namespaces.
- Validate ontology syntax and expected structure.
- Report malformed or incompatible elements.
- Compare ontology versions at node level.
- Generate CDuce verification and transformation programs from templates.
- Apply assisted corrections and save the resulting ontology.
- Record timestamped application logs.
- Test the XML utilities, middleware, and command-execution layer.

## Architecture

The application is organized into five main areas:

- **GUI** — JavaFX controllers, FXML views, and styles.
- **Middleware** — coordinates user actions and the validation/transformation workflow.
- **CDuce integration** — loads templates, replaces placeholders, and executes generated CDuce programs.
- **XML utilities** — formatting, XPath parsing, difference checking, and error reporting.
- **Data model** — ontologies, edits, structural checks, and error information.

## Requirements

- JDK 23, as configured in the Maven compiler properties.
- Apache Maven.
- JavaFX 17.0.2, resolved through Maven.
- CDuce installed in a Linux or WSL environment.
- A configured .env file containing the paths used by the application.

The command-execution layer converts Windows paths to WSL paths, so the current integration is primarily designed for Windows with WSL.

## Configuration

Copy the supplied template before running the application:

    cp .env_template .env

Then replace every PATH placeholder with a valid path for your machine.

| Variable | Purpose |
| --- | --- |
| LOG_PATH | Directory used for application logs. |
| CDUCE_CODE_PATH | Project-relative directory for generated CDuce files. |
| CDUCE_TEMPLATE_PATH | Path to the JSON placeholder-definition file. |
| CDUCE_CODE_PATH_ABSOLUTE | Absolute CDuce source directory used during execution. |
| ONTOLOGY_INPUT | Project-relative temporary input ontology. |
| ONTOLOGY_INPUT_ABSOLUTE | Absolute input ontology path, accessible from CDuce. |
| ONTOLOGY_OUTPUT_ABSOLUTE | Absolute destination for transformed ontologies. |

The repository includes the base CDuce template and substitution map under src/main/resources/cducesourcecode.

## Build and Test

Resolve dependencies, compile the application, and run the test suite:

    mvn clean test

Build the project without running tests:

    mvn clean package -DskipTests

The current pom.xml does not configure a JavaFX launcher plugin or an executable JAR. The most reliable way to start the project is therefore to import it as a Maven project in an IDE and run:

    com.jataxmltransformer.main.Main

If launching from the command line, configure the JavaFX module path for your local JavaFX installation and use the same main class.

## Screenshots

![Application icon](images/app_icon.png)

![Namespace management](images/namespacesFrame.png)

![Structure validation](images/structureFrame.png)

![Syntax error reporting](images/syntaxError.png)

![Ontology editor](images/singleclass2.png)

![Validated ontology](images/correctOntology.png)

## Repository Structure

    .
    ├── pom.xml
    ├── .env_template
    ├── images/
    └── src/
        ├── main/
        │   ├── java/com/jataxmltransformer/
        │   │   ├── GUI/
        │   │   ├── logic/
        │   │   ├── logs/
        │   │   ├── main/
        │   │   └── middleware/
        │   └── resources/
        │       ├── GUI/
        │       ├── cducesourcecode/
        │       └── images/
        └── test/java/

## Related Work

- [Ontology transformation scripts](https://github.com/FurTh3r/ontology-transformation-cduce)
- [CDuce syntax highlighting for VS Code](https://github.com/FurTh3r/cduce-syntax-highlighting)
- [Bachelor's thesis](https://github.com/FurTh3r/batchelor_thesis)

## Author

**Lorenzo Pasini** — [FurTh3r](https://github.com/FurTh3r)

## License

No license file is currently included in this repository. Unless otherwise stated by the author, all rights are reserved.
