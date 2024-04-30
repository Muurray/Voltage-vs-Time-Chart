# Voltage-vs-Time-Chart
An app for plotting the Voltage vs Time Chart
classdef Calibration < matlab.apps.AppBase

    % Properties that correspond to app components
    properties (Access = public)
        UIFigure                      matlab.ui.Figure
        GridLayout                    matlab.ui.container.GridLayout
        InputDatayaxisEditField       matlab.ui.control.NumericEditField
        InputDatayaxisEditFieldLabel  matlab.ui.control.Label
        InputDataxaxisEditField       matlab.ui.control.NumericEditField
        InputDataxaxisEditFieldLabel  matlab.ui.control.Label
        TroughPointsButton            matlab.ui.control.Button
        PeakPointsButton              matlab.ui.control.Button
        AverageButton                 matlab.ui.control.Button
        UIAxes                        matlab.ui.control.UIAxes
        ContextMenu                   matlab.ui.container.ContextMenu
        Menu                          matlab.ui.container.Menu
        Menu2                         matlab.ui.container.Menu
    end

    
    methods (Access = public)
        
        function results = func(app)
            
        end
        
    end
    
    methods (Access = private)
        
    end
    

    % Callbacks that handle component events
    methods (Access = private)

        % Code that executes after component creation
        function startupFcn(app, average)
            
        end

        % Button pushed function: AverageButton
        function AverageButtonPushed(app, event)
            
        end

        % Value changed function: InputDataxaxisEditField
        function InputDataxaxisEditFieldValueChanged(app, event)
            value = app.InputDataxaxisEditField.Value;
            
        end
    end

    % Component initialization
    methods (Access = private)

        % Create UIFigure and components
        function createComponents(app)

            % Create UIFigure and hide until all components are created
            app.UIFigure = uifigure('Visible', 'off');
            colormap(app.UIFigure, 'jet');
            app.UIFigure.Position = [100 100 640 480];
            app.UIFigure.Name = 'MATLAB App';

            % Create GridLayout
            app.GridLayout = uigridlayout(app.UIFigure);
            app.GridLayout.ColumnWidth = {'1x', 100, 26, 100, '1.48x', 124, '5.92x'};
            app.GridLayout.RowHeight = {'11.56x', '2.13x', 23, '1.44x', 22, '1x', 22, '4.06x'};
            app.GridLayout.BackgroundColor = [0.8 0.8 0.8];

            % Create UIAxes
            app.UIAxes = uiaxes(app.GridLayout);
            title(app.UIAxes, 'Voltage vs Time')
            xlabel(app.UIAxes, 'Time')
            ylabel(app.UIAxes, 'voltage')
            zlabel(app.UIAxes, 'Z')
            app.UIAxes.Layout.Row = 1;
            app.UIAxes.Layout.Column = [2 6];
            colormap(app.UIAxes, 'jet')

            % Create AverageButton
            app.AverageButton = uibutton(app.GridLayout, 'push');
            app.AverageButton.ButtonPushedFcn = createCallbackFcn(app, @AverageButtonPushed, true);
            app.AverageButton.IconAlignment = 'center';
            app.AverageButton.WordWrap = 'on';
            app.AverageButton.BackgroundColor = [1 0.0745 0.651];
            app.AverageButton.FontName = 'Impact';
            app.AverageButton.FontWeight = 'bold';
            app.AverageButton.FontColor = [0 0 1];
            app.AverageButton.Layout.Row = 3;
            app.AverageButton.Layout.Column = 2;
            app.AverageButton.Text = 'Average';

            % Create PeakPointsButton
            app.PeakPointsButton = uibutton(app.GridLayout, 'push');
            app.PeakPointsButton.BackgroundColor = [1 0.0745 0.651];
            app.PeakPointsButton.FontWeight = 'bold';
            app.PeakPointsButton.FontColor = [0 1 0];
            app.PeakPointsButton.Layout.Row = 3;
            app.PeakPointsButton.Layout.Column = 4;
            app.PeakPointsButton.Text = 'Peak Points';

            % Create TroughPointsButton
            app.TroughPointsButton = uibutton(app.GridLayout, 'push');
            app.TroughPointsButton.BackgroundColor = [1 0.0745 0.651];
            app.TroughPointsButton.FontWeight = 'bold';
            app.TroughPointsButton.FontColor = [1 1 0];
            app.TroughPointsButton.Layout.Row = 3;
            app.TroughPointsButton.Layout.Column = 6;
            app.TroughPointsButton.Text = 'Trough Points';

            % Create InputDataxaxisEditFieldLabel
            app.InputDataxaxisEditFieldLabel = uilabel(app.GridLayout);
            app.InputDataxaxisEditFieldLabel.BackgroundColor = [0 1 0];
            app.InputDataxaxisEditFieldLabel.HorizontalAlignment = 'right';
            app.InputDataxaxisEditFieldLabel.FontSize = 14;
            app.InputDataxaxisEditFieldLabel.FontWeight = 'bold';
            app.InputDataxaxisEditFieldLabel.FontAngle = 'italic';
            app.InputDataxaxisEditFieldLabel.FontColor = [0 0 1];
            app.InputDataxaxisEditFieldLabel.Layout.Row = 5;
            app.InputDataxaxisEditFieldLabel.Layout.Column = [2 3];
            app.InputDataxaxisEditFieldLabel.Text = 'Input Data (x-axis)';

            % Create InputDataxaxisEditField
            app.InputDataxaxisEditField = uieditfield(app.GridLayout, 'numeric');
            app.InputDataxaxisEditField.ValueChangedFcn = createCallbackFcn(app, @InputDataxaxisEditFieldValueChanged, true);
            app.InputDataxaxisEditField.HandleVisibility = 'callback';
            app.InputDataxaxisEditField.FontAngle = 'italic';
            app.InputDataxaxisEditField.BackgroundColor = [0 1 1];
            app.InputDataxaxisEditField.Layout.Row = 5;
            app.InputDataxaxisEditField.Layout.Column = 4;

            % Create InputDatayaxisEditFieldLabel
            app.InputDatayaxisEditFieldLabel = uilabel(app.GridLayout);
            app.InputDatayaxisEditFieldLabel.BackgroundColor = [0 1 0];
            app.InputDatayaxisEditFieldLabel.HorizontalAlignment = 'right';
            app.InputDatayaxisEditFieldLabel.FontSize = 14;
            app.InputDatayaxisEditFieldLabel.FontWeight = 'bold';
            app.InputDatayaxisEditFieldLabel.FontColor = [0 0 1];
            app.InputDatayaxisEditFieldLabel.Layout.Row = 7;
            app.InputDatayaxisEditFieldLabel.Layout.Column = [2 3];
            app.InputDatayaxisEditFieldLabel.Text = 'Input Data (y-axis)';

            % Create InputDatayaxisEditField
            app.InputDatayaxisEditField = uieditfield(app.GridLayout, 'numeric');
            app.InputDatayaxisEditField.FontWeight = 'bold';
            app.InputDatayaxisEditField.BackgroundColor = [0.0588 1 1];
            app.InputDatayaxisEditField.Layout.Row = 7;
            app.InputDatayaxisEditField.Layout.Column = 4;

            % Create ContextMenu
            app.ContextMenu = uicontextmenu(app.UIFigure);

            % Create Menu
            app.Menu = uimenu(app.ContextMenu);
            app.Menu.Text = 'Menu';

            % Create Menu2
            app.Menu2 = uimenu(app.ContextMenu);
            app.Menu2.Text = 'Menu2';

            % Show the figure after all components are created
            app.UIFigure.Visible = 'on';
        end
    end

    % App creation and deletion
    methods (Access = public)

        % Construct app
        function app = Calibration(varargin)

            % Create UIFigure and components
            createComponents(app)

            % Register the app with App Designer
            registerApp(app, app.UIFigure)

            % Execute the startup function
            runStartupFcn(app, @(app)startupFcn(app, varargin{:}))

            if nargout == 0
                clear app
            end
        end

        % Code that executes before app deletion
        function delete(app)

            % Delete UIFigure when app is deleted
            delete(app.UIFigure)
        end
    end
end
