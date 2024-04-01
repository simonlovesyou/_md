### Metadata Configuration

Users can define custom metadata configurations in JSON format to specify which fields to measure and how to interpret the data. The tool includes default metadata configurations for common file types, but users can create their own configurations or download them from npm.

### Measurement Collection

The tool allows the user to do arbitrary measurements and store these measurements as metadata for a commit or tag. Each measurement is associated with a metadata configuration, which allows for interpretation and comparison of measurements.

### Plugins

Plugins can be made

### Usage

```JavaScript
import createConfig from '@metada/config'
import fileSizePlugin from '@metada/plugins/file-size'

export default createConfig({
  plugins: [fileSizePlugin({
    files: ["./dist/**/*.js"]
  })]
})
```

### Creating a plugin

A plugin is created by exposing a function that accepts options as first argument, and then it must return an object that contains:  
  

### Comparison

Users can compare multiple measurements by running the `metadata compare` command. The tool can display the differences between measurements in various formats, including human-readable strings, tables, and CSV files. Users can customize the output format by specifying options in the command-line interface or programmatically using the provided API.

### Customization

Users can customize the metadata configurations and output formats to suit their needs. They can override the default metadata configuration settings or customize the diff output through the CLI or programmatic API. The tool stores the customization settings locally for future use.

The `metadata` makes it easy to track changes in metadata across code repository versions and quickly identify any differences in metadata. It provides a flexible and customizable way to measure and compare metadata that can save developers valuable time and effort.