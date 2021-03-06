## API Report File for "@microsoft/ts-command-line"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts

import * as argparse from 'argparse';

// @public
export abstract class CommandLineAction extends CommandLineParameterProvider {
    constructor(options: ICommandLineActionOptions);
    readonly actionName: string;
    // @internal
    _buildParser(actionsSubParser: argparse.SubParser): void;
    readonly documentation: string;
    // @internal
    _execute(): Promise<void>;
    // @internal
    protected _getArgumentParser(): argparse.ArgumentParser;
    protected abstract onDefineParameters(): void;
    protected abstract onExecute(): Promise<void>;
    // @internal
    _processParsedData(data: _ICommandLineParserData): void;
    readonly summary: string;
}

// @public
export class CommandLineChoiceParameter extends CommandLineParameter {
    // @internal
    constructor(definition: ICommandLineChoiceDefinition);
    readonly alternatives: ReadonlyArray<string>;
    // @override
    appendToArgList(argList: string[]): void;
    readonly defaultValue: string | undefined;
    // @internal
    _getSupplementaryNotes(supplementaryNotes: string[]): void;
    readonly kind: CommandLineParameterKind;
    // @internal
    _setValue(data: any): void;
    readonly value: string | undefined;
    }

// @public
export class CommandLineFlagParameter extends CommandLineParameter {
    // @internal
    constructor(definition: ICommandLineFlagDefinition);
    // @override
    appendToArgList(argList: string[]): void;
    readonly kind: CommandLineParameterKind;
    // @internal
    _setValue(data: any): void;
    readonly value: boolean;
    }

// @public
export class CommandLineIntegerParameter extends CommandLineParameterWithArgument {
    // @internal
    constructor(definition: ICommandLineIntegerDefinition);
    // @override
    appendToArgList(argList: string[]): void;
    readonly defaultValue: number | undefined;
    // @internal
    _getSupplementaryNotes(supplementaryNotes: string[]): void;
    readonly kind: CommandLineParameterKind;
    // @internal
    _setValue(data: any): void;
    readonly value: number | undefined;
    }

// @public
export abstract class CommandLineParameter {
    // @internal
    constructor(definition: IBaseCommandLineDefinition);
    abstract appendToArgList(argList: string[]): void;
    readonly description: string;
    readonly environmentVariable: string | undefined;
    // @internal
    _getSupplementaryNotes(supplementaryNotes: string[]): void;
    abstract readonly kind: CommandLineParameterKind;
    readonly longName: string;
    // @internal
    _parserKey: string;
    protected reportInvalidData(data: any): never;
    readonly required: boolean;
    // @internal
    abstract _setValue(data: any): void;
    readonly shortName: string | undefined;
    // (undocumented)
    protected validateDefaultValue(hasDefaultValue: boolean): void;
}

// @public
export enum CommandLineParameterKind {
    Choice = 0,
    Flag = 1,
    Integer = 2,
    String = 3,
    StringList = 4
}

// @public
export abstract class CommandLineParameterProvider {
    // @internal
    constructor();
    defineChoiceParameter(definition: ICommandLineChoiceDefinition): CommandLineChoiceParameter;
    defineFlagParameter(definition: ICommandLineFlagDefinition): CommandLineFlagParameter;
    defineIntegerParameter(definition: ICommandLineIntegerDefinition): CommandLineIntegerParameter;
    defineStringListParameter(definition: ICommandLineStringListDefinition): CommandLineStringListParameter;
    defineStringParameter(definition: ICommandLineStringDefinition): CommandLineStringParameter;
    // @internal
    protected abstract _getArgumentParser(): argparse.ArgumentParser;
    getChoiceParameter(parameterLongName: string): CommandLineChoiceParameter;
    getFlagParameter(parameterLongName: string): CommandLineFlagParameter;
    getIntegerParameter(parameterLongName: string): CommandLineIntegerParameter;
    getStringListParameter(parameterLongName: string): CommandLineStringListParameter;
    getStringParameter(parameterLongName: string): CommandLineStringParameter;
    protected abstract onDefineParameters(): void;
    readonly parameters: ReadonlyArray<CommandLineParameter>;
    // @internal (undocumented)
    protected _processParsedData(data: _ICommandLineParserData): void;
    renderHelpText(): string;
}

// @public
export abstract class CommandLineParameterWithArgument extends CommandLineParameter {
    // @internal
    constructor(definition: IBaseCommandLineDefinitionWithArgument);
    readonly argumentName: string;
    }

// @public
export abstract class CommandLineParser extends CommandLineParameterProvider {
    constructor(options: ICommandLineParserOptions);
    readonly actions: ReadonlyArray<CommandLineAction>;
    addAction(action: CommandLineAction): void;
    execute(args?: string[]): Promise<boolean>;
    executeWithoutErrorHandling(args?: string[]): Promise<void>;
    getAction(actionName: string): CommandLineAction;
    // @internal
    protected _getArgumentParser(): argparse.ArgumentParser;
    protected onExecute(): Promise<void>;
    selectedAction: CommandLineAction | undefined;
    readonly toolDescription: string;
    readonly toolFilename: string;
    tryGetAction(actionName: string): CommandLineAction | undefined;
}

// @public
export class CommandLineStringListParameter extends CommandLineParameterWithArgument {
    // @internal
    constructor(definition: ICommandLineStringListDefinition);
    // @override
    appendToArgList(argList: string[]): void;
    readonly kind: CommandLineParameterKind;
    // @internal
    _setValue(data: any): void;
    readonly values: ReadonlyArray<string>;
    }

// @public
export class CommandLineStringParameter extends CommandLineParameterWithArgument {
    // @internal
    constructor(definition: ICommandLineStringDefinition);
    // @override
    appendToArgList(argList: string[]): void;
    readonly defaultValue: string | undefined;
    // @internal
    _getSupplementaryNotes(supplementaryNotes: string[]): void;
    readonly kind: CommandLineParameterKind;
    // @internal
    _setValue(data: any): void;
    readonly value: string | undefined;
    }

// @public (undocumented)
export class DynamicCommandLineAction extends CommandLineAction {
    // (undocumented)
    protected onDefineParameters(): void;
    // (undocumented)
    protected onExecute(): Promise<void>;
}

// @public (undocumented)
export class DynamicCommandLineParser extends CommandLineParser {
    // (undocumented)
    protected onDefineParameters(): void;
}

// @public
export interface IBaseCommandLineDefinition {
    description: string;
    environmentVariable?: string;
    parameterLongName: string;
    parameterShortName?: string;
    required?: boolean;
}

// @public
export interface IBaseCommandLineDefinitionWithArgument extends IBaseCommandLineDefinition {
    argumentName: string;
}

// @public
export interface ICommandLineActionOptions {
    actionName: string;
    documentation: string;
    summary: string;
}

// @public
export interface ICommandLineChoiceDefinition extends IBaseCommandLineDefinition {
    alternatives: string[];
    defaultValue?: string;
}

// @public
export interface ICommandLineFlagDefinition extends IBaseCommandLineDefinition {
}

// @public
export interface ICommandLineIntegerDefinition extends IBaseCommandLineDefinitionWithArgument {
    defaultValue?: number;
}

// @internal
export interface _ICommandLineParserData {
    // (undocumented)
    [key: string]: any;
    // (undocumented)
    action: string;
}

// @public
export interface ICommandLineParserOptions {
    toolDescription: string;
    toolFilename: string;
}

// @public
export interface ICommandLineStringDefinition extends IBaseCommandLineDefinitionWithArgument {
    defaultValue?: string;
}

// @public
export interface ICommandLineStringListDefinition extends IBaseCommandLineDefinitionWithArgument {
}


```
